pipeline {
    agent any
 
    tools {nodejs "node"}
 
    stages {
 
        stage('Cloning Git') {
            steps {
                git 'https://github.com/mahsankhaan/kubernetes_with_jenkins.git'
            }
        }
    }
}
