pipeline {
    agent any

    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh(script: 'docker-compose build')
            }
        }
        stage('Start App') {
            steps {
                sh(script: 'docker-compose up -d')
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
            sh(script: 'docker-compose down')
        }
    }
}