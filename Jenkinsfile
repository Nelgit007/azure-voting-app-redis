pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Shutdown docker compose') {
            steps {
                sh(script: 'docker-compose down -v')
            }
        }
        stage('Docker Build') {
            steps {
                sh(script: 'docker-compose build')
            }
        }
        stage('Start App') {
            steps {
                sh(script: 'docker-compose up -d --publish-all')
            }
        }
        stage('Run Test') {
            steps {
                sh(script: 'pytest ./feature/test_sample.py')
            }
            post {
                success {
                    echo "Test passed! :)"
                }
                failure {
                    echo "Test Failed! :("
                }
            }
        }
    }
    post {
        always {
            sh(script: 'docker-compose down -v --rmi all')
        }
    }
}