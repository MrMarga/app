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

        stage('Sonar Analysis')
            {
                steps{
                    sh"mvn clean pacakge"
                    sh""" mvn sonar:sonar -Dsonar.url=http://192.168.100.54:8081 -Dsonar.login=squ_45ace6d0f27c0b304f7347cd04663d6044104720"""
                }
            }
    }
}