pipeline {
    agent any

    environment {
        dockerregistry = 'https://registry.hub.docker.com'
        dockerhuburl = "ahsanoffical/jenkins"
        githuburl = "mahsankhaan/kubernetes_with_jenkins"
        dockerhubcredentials = 'dockerhub'
    }
    tools {nodejs "node"}
 
   stages {
 
        stage('Clone git repo') {
            steps {
                   git 'https://github.com/mahsankhaan/kubernetes_with_jenkins.git'

            }
        }
 
        stage('Install Node.js dependencies') {
            steps {
                sh 'npm install'
            }
        }
 
        stage('Build image') {
          steps{
            script {
               dockerImage = docker.build dockerhuburl + ":$BUILD_NUMBER"

            }
          }
        }
 
        stage('Deploy image') {
          steps{
            script {
              docker.withRegistry(dockerregistry, dockerhubcredentials ) {
                dockerImage.push("${env.BUILD_NUMBER}")
                dockerImage.push("latest")
              }
            }
          }
        }
 
        stage('Remove image') {
          steps{
            sh "docker rmi $dockerhuburl:$BUILD_NUMBER"
          }
      
}
   }
   }
