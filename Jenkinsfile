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
                    sh 'sudo apt-get update && sudo apt-get install docker'
                    
            script {
                  def newApp = docker.build "ahsanoffical/jenkins:${env.BUILD_TAG}"

            }
          }
        }
 
   }
 }
   
