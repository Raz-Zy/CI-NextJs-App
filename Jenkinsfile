pipeline{
    agent any
    environment{
        DOCKER_FILE = "Dockerfile"
    }
    stages{
        stage("Build Image"){
            steps{
                script{
                    echo "Build nextjs image."
                    sh 'docker build -t nextjs-image .'
                }
            }
        }
    }
}