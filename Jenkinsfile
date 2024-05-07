pipeline {
    agent any
    
    stages {
        stage('clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'jenkins --version'
                sh 'docker --version'
            }
        }
        stage('Checkout from Git') {                        
            steps {                                       
                git branch: 'main', url: 'https://github.com/yash509/DevOps-Task-1-Intern_Career.git'
            }
        }
        stage("Docker Image Building"){
            steps{
                script{
                    //dir('Band Website') {
                        withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                            sh "docker build -t ice-cream-parlor ." 
                            
                        //}
                    }
                }
            }
        }
        stage("Docker Image Tagging"){
            steps{
                script{
                        withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
                            sh "docker tag ice-cream-parlor yash5090/ice-cream-parlor:latest "
                    }
                }
            }
        } 
        stage("Image Push to DockerHub") {
            steps{
                script{
                  withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                    sh "docker push yash5090/ice-cream-parlor:latest "
                  }
                }
            }
        }
        stage('Deploy to Docker Container'){
            steps{
              sh 'docker run -d --name ice-cream-parlor -p 3000:80 yash5090/ice-cream-parlor:latest' 
            }
        }
    }
}
