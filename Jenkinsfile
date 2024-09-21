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
        stage("Update to image in the kubernetes manifest file to latest images"){
            steps{
                script{
                    git credentialsId: 'git-token', url: 'https://github.com/Raz-Zy/CD-NextJS-Helm.git'
                    echo "Update Image Tag"
                    sh 'sed -i "s/tag:.*/tag: ${TAG}.${VERSION}/" values.yaml'
                    echo "Git Config for pushing latest update."
                    sh "git config --global user.email 'tandara120403@gmail.com'"
                    sh "git config --global user.name 'Tan Dara'"
                    sh "git commit -am 'Update image tag'"
                    sh "git push origin master"
                }
            }
        }
    }
}