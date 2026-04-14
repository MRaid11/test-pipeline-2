pipeline {
    agent any

    tools {
        jdk "JAVA_HOME"
    }

    environment {
        DOCKER_IMAGE = "dweeb3391/myapp"
        DOCKER_TAG = "latest"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/MRaid11/test-pipeline-2.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $DOCKER_IMAGE:$DOCKER_TAG ."
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'dweeb3391',
                    passwordVariable: 'Atalanta5566@'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push $DOCKER_IMAGE:$DOCKER_TAG"
            }
        }
    }

    post {
        success {
            echo "Build & Docker push completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
