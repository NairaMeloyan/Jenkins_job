pipeline {
    agent any

    // environment {
    //     registry = "060787452196.dkr.ecr.eu-central-1.amazonaws.com/project"
    // }

    stages {
        stage("verity tooling") {
            steps {
                sh '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                    jq --version
                '''
            }
        }

        stage('Building image') {
            steps {
                script {
                    dockerImage = naramelo/exammongo:v1.7
                }
            }
        }

        stage("start container") {
            steps {
                sh 'docker compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }

        stage("run tests against container") {
            steps {
                sh 'curl http://localhost:8081/param?query=demo | jq'
            }
        }
    }
}
