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
 
       stage('Deploy k8s') {
      steps {
        kubernetesDeploy(
          kubeconfigId: 'k8s',
          configs: 'k8s.yaml',
          enableConfigSubstitution: true
        )
      }
    }
 
 
   
 }
 }
