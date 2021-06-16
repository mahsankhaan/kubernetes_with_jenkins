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
 
   stage('Apply Kubernetes Files') {
      steps {
          withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'kubectl get pods -n jenkins'
        }
      }
 
 }
 }
 }
