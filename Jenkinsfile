pipeline {
    agent any

    environment {
        IMAGE_NAME = 'myapp'
        IMAGE_TAG = 'latest'
        REGISTRY = 'kshitija1510'
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
                    sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'docker run --rm $IMAGE_NAME:$IMAGE_TAG'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        sh 'docker tag $IMAGE_NAME:$IMAGE_TAG $REGISTRY/$IMAGE_NAME:$IMAGE_TAG'
                        sh 'docker push $REGISTRY/$IMAGE_NAME:$IMAGE_TAG'
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
