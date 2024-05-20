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
                powershell(script : '$Env:DOCKER_SCAN_SUGGEST = "false"; docker compose build')
            }
        }
        stage('Start App'){
            steps{
                powershell(script : 'docker compose -d')
            }
        }
        stage('Run tests'){
            steps{
                powershell(script : 'pytests ./tests/test-sample')
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
            powershell(script : 'docker compose down')
        }
    } 
}

//start app  || run test