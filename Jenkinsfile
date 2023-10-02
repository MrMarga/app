pipeline {
    agent any
    environment{DOCKERHUB_CREDENTIALS = credentials('docker')}
    
    stages{
        stage("Code"){
           steps{
                git url: "https://github.com/MrMarga/emartapp.git", branch: "main"
            }
        }
        stage("Build & Test"){
           steps{
                sh "docker build . -t emart-new "
                sh "docker-compose build "
            }
        }
        stage('Push to Docker Hub') {
           steps {
                 echo "Pushing the image to docker hub"
                    sh "docker tag emart-new $DOCKERHUB_CREDENTIALS_USR/emart-new:latest"
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                    sh "docker push $DOCKERHUB_CREDENTIALS_USR/emart-new:latest"
                     }
            }

        stage("Deploy"){
           steps{
                sh "docker-compose up -d   "}
                }

        post {
        always {
            echo 'Slack Notifications.'
            slackSend channel: '#jenkinscicd',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} \n More info at: ${env.BUILD_URL}"
            }
         }
    }
}