pipeline {
    agent any

    stages {
        stage('Compile and Test') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/zainwaseem/spock-lizard-docker-jenkins.git'

                // Run Maven
                bat "mvn clean compile test"
            }
        }
        stage('Build Spring Boot Jar') {
            steps {
                bat "mvn clean package spring-boot:repackage"
            }
        }
        stage('Create Docker Image') {
            steps {
                bat "docker build -t zainwaseem/rps-for-jenkins-tut:latest ."
            }
        }
        stage('Deploy to DockerHub') {
            steps {
                script {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', 
                                              usernameVariable: 'USERNAME', 
                                              passwordVariable: 'PASSWORD')]) {
                bat "docker login --username %USERNAME% --password %PASSWORD%"
                bat "docker push zainwaseem/rps-for-jenkins-tut:latest"
            }
                }
            }
        } // <-- This closing bracket was missing
    }
}
