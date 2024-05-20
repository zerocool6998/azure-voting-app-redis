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
    }
}