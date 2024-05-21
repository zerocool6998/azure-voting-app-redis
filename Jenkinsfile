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
                sh(script : '$Env:DOCKER_SCAN_SUGGEST = "false"; docker compose build')
            }
        }
        stage('Start App'){
            steps{
                sh(script : 'docker compose up -d')
            }
        }
    
        stage('Run tests'){
            steps{
                sh(script : 'pytest ./tests/test-sample.py')
            }
            post{
                success{
                    echo "test passed :)"
                }
                failure{
                    echo "test failed :("
                }
            }

        }

    }
    post{
        always{
            sh(script : 'docker compose down')
        }
    } 
}

//start app  || run test