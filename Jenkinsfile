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
                    // ✅ Use current directory as context since Dockerfile is in repo root
                    sh 'docker build -t myapp:latest .'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add test scripts here if any
            }
        }

        stage('Push to DockerHub') {
            steps {
                script {
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh 'docker tag myapp:latest yourdockerhubusername/myapp:latest'
                    sh 'docker push yourdockerhubusername/myapp:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add your deployment logic here
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
