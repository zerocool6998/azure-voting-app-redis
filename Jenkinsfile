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
                sh 'pip install pytest'
            }
        }
    
        // stage('Run tests'){
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

        // }

        stage('Docker push'){
            steps{
                echo "Running in $WORKSPACE"
                dir("$WORKSPACE/azure-vote") {
                    script {
                        docker.withRegistry('','jenkins-zerocool12'){
                            def image = docker.build('zerocool12/jenkins_pipeline:2024')
                            image.push()
                        }
                    }
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