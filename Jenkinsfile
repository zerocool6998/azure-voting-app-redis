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
                powershell(script : 'docker compose up -d')
            }
        }
        stage('Adding Pytest'){
            steps{
                // powershell(script : 'pip install pytest')
                bat 'powershell.exe -NoProfile -NonInteractive -ExecutionPolicy Bypass -Command "<your PowerShell command>"'
                bat 'powershell.exe -NoProfile -NonInteractive -ExecutionPolicy Bypass -Command "pip install pytest"'
            }
        }
        stage('Run tests'){
            steps{
                powershell(script : 'pytest ./tests/test-sample.py')
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