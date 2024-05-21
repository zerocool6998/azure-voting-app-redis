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
                sh(script : 'docker compose build')
            }
        }
        stage('Start App'){
            steps{
                sh(script : 'docker compose up -d')
            }
        }
        stage('Pytest'){
            steps{
                sh(script : 'pip install pytest')
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