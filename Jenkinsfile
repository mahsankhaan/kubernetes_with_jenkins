podTemplate(
    cloud: 'kubernetes',
    label: 'workshop',
    containers: [
     containerTemplate(
                    image: 'docker', 
                    name: 'docker', 
                    command: 'cat', 
                    ttyEnabled: true

                    ),
               ],
    volumes: [
        hostPathVolume(
            mountPath: '/var/run/docker.sock',
            hostPath: '/var/run/docker.sock'
        )
    ]
)
{
  node("workshop") {
        stage('Build') {
            git url: 'https://github.com/mahsankhaan/kubernetes_with_jenkins.git'
            container('docker') {
                sh ' docker build -t getting-started .'
            }
        }
  }
}



