podTemplate(
    cloud: 'kubernetes',
    label: 'workshop',
    containers: [
        containerTemplate(
            name: 'nodejs',
            image:'node:alpine',
            ttyEnabled: true,
            alwaysPullImage: false
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
    agent any {
        stage('Test') {
            git url: 'https://github.com/volaka/jenkins-nodejs-app.git'
            container('nodejs') {
                sh 'npm install'
                sh 'npm run test'
            }
        }
        
}
}
