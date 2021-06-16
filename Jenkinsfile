pipeline {
  agent any
  stages {
    
    stage('Apply Kubernetes Files') {
      steps {
          withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'kubectl version'
        }
      }
  }
}
}
