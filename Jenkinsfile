pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
    }

    stages {
        stage('Clone Repo') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/Kshitija-0710/Jenkins.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    // Assuming Dockerfile is in Jenkins/ directory inside the repo
                    sh 'docker build -t myapp:latest Jenkins/'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your test commands here
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                    sh 'docker tag myapp:latest kshitija1510/myapp:latest'
                    sh 'docker push kshitija1510/myapp:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add your deployment steps here
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
