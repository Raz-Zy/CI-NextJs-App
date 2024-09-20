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
                    echo "build number: ${VERSION}"
                }
            }
        }
    }
}