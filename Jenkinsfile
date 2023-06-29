pipeline {
    agent any
    
    stages {
        stage('git checkout') {
            steps {
                git credentialsId: '959fb1a5-310b-47bc-975c-cd96e7001b60', url: 'https://github.com/Baldton/magasin_informatique'
            }
        }
        
        stage('Build the application') {
            steps {
                bat 'mvn clean install' // Utilisez 'bat' pour exécuter des commandes PowerShell sous Windows
            }
        }
        
        stage('Unit Test Execution') {
            steps {
                bat 'mvn test'
            }
        }
        
        stage('Build the docker image') {
            steps {
                script {
                    dockerImage = docker.build("geinn/pipeline-triangle")
                }
            }
        }
        
        stage('Build and push the docker image to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: "dockerhubaccount", url: "https://registry.hub.docker.com"]) {
                    script {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}