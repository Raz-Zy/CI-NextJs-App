pipeline{
    agent any
    environment{
        DOCKER_FILE = "Dockerfile"
        IMAGE = "razzy10/nextjs-app-image"
        TAG = "0.0"
        VERSION = "${env.Build_ID}"
    }
    stages{
        stage("Build Image"){
            steps{
                script{
                    echo "Build nextjs image."
                    sh "docker build -t ${IMAGE}:${TAG}.${VERSION} ."
                }
            }
        }
        stage("Push image to registry (Docker Hub)"){
            steps{
                script{
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-token', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                        echo "Login Docker Hub"
                        sh "docker login -u $USERNAME -p $PASSWORD"
                        sh "docker push ${IMAGE}:${TAG}.${VERSION}"
                    }
                }
            }
        }
    }
}