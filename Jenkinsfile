pipeline {
  agent any

  stages {
    stage('Test') {
      steps {
        container('nodejs') {
          sh "node --version"
        }
      }
    }
  }
}
