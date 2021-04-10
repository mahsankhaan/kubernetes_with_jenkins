def gitSHA

pipeline {
  agent {
    kubernetes {
      defaultContainer 'jnlp'
    }
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        script {
          gitSHA = sh(returnStdout: true, script: 'git rev-parse --short HEAD')
        }
      }
    }
    stage('Test') {
      steps {
        container('nodejs') {
          sh "node --version"

        }
      }
    }