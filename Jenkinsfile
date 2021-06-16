podTemplate(
    cloud: 'kubernetes',
    label: 'workshop',
    containers: [
        containerTemplate(
            name: 'nodejs',
            image:'node:alpine',
            ttyEnabled: true,
            alwaysPullImage: false
        ) 
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
        stage('Test') {
            git url: 'https://github.com/mahsankhaan/kubernetes_with_jenkins.git'
            container('nodejs') {
                sh 'npm install'
                sh 'npm run test'
            }
        }
    }
}
