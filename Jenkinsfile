pipeline {
    agent any
    
    stages {
        stage('Code'){
            steps{
                git url: 'https://github.com/Chandu-Ram/node-todo-cicd.git', branch: 'master'
            }
            
        }
        stage('Build'){
            steps{
                sh 'docker build . -t kubechandu7/node-todo-test:latest' 
            }
        }
        stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) 
                {
                 sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                 sh 'docker push kubechandu7/node-todo-test:latest'
                }
            }
            
        }
        stage('Test'){
            steps{
                echo "Testing the build......No Test Cases" 
            }
            
        }
        stage('Deploy'){
            steps{
                sh "docker-compose down && docker-compose build --no-cache && docker-compose up -d" 
            }
            
        }
    }
}
