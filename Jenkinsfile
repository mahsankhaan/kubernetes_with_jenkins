podTemplate(
    cloud: 'kubernetes',
    label: 'workshop',
    containers: [
     tainerTemplate(
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
 
        stage('Build') {
            git url: 'https://github.com/mahsankhaan/kubernetes_with_jenkins.git'
            container('docker') {
                sh 'systemctl start docker'
                sh 'docker version'
            }
        }
    }
}



