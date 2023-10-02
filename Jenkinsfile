pipeline {
    agent any
    
    tools{
        jdk "jdk11"
        maven "maven3"
    }

    stages{

        stage('Git Checkout')
            {
            steps{
                git url:"https://github.com/MrMarga/app.git",branch:"main"
            }
        }

        stage('MVN testings')
            {
                steps{
                    sh"mvn test"
                }
            }
    }
}