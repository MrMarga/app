pipeline {
    agent any
    environment{DOCKERHUB_CREDENTIALS = credentials('docker')}
    
    stages{
        
        stage("Code"){
            steps{
                git url: "https://github.com/MrMarga/todo.git", branch: "main"
            }
        }
        stage("Build & Test"){
            steps{
                 sh "docker-compose build"
                 sh "docker build . -t emart-new"
                 
            }
        }
        stage('Push to Docker Hub') {
            steps {
                 echo "Pushing the images to docker hub"
                    sh "docker tag emart-new $DOCKERHUB_CREDENTIALS_USR/emart-new:latest"
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker push $DOCKERHUB_CREDENTIALS_USR/emart-new:latest"
                     } 
            }

        stage("Deploy"){
            steps{
                sh "docker-compose up -d "
            }
        }
    }
}