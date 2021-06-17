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
        containerTemplate(
            name: 'build',
            image: 'ibmcom/ibm-cloud-developer-tools-amd64',
            ttyEnabled: true,
            alwaysPullImage: false,
            envVars: [
                secretEnvVar(
                    key: 'REGISTRY_TOKEN',
                    secretName: 'ibm-cloud-api-key',
                    secretKey: 'apikey'
                )
            ]
        ),
        containerTemplate(
            name: 'deploy',
            image: 'ibmcom/ibm-cloud-developer-tools-amd64',
            ttyEnabled: true,
            alwaysPullImage: false,
            envVars: [
                secretEnvVar(
                    key: 'IBMCLOUD_TOKEN',
                    secretName: 'ibm-cloud-api-key',
                    secretKey: 'apikey'
                )
            ]
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
        stage('Test') {
            git url: 'https://github.com/volaka/jenkins-nodejs-app.git'
            container('nodejs') {
                sh 'npm install'
                sh 'npm run test'
            }
        }
        stage('Build') {
            git url: 'https://github.com/volaka/jenkins-nodejs-app.git'
            container('build') {
                sh 'ibmcloud login -a cloud.ibm.com -r eu-de --apikey ${REGISTRY_TOKEN}'
                sh 'ibmcloud cr login'
                sh 'ibmcloud cr build -t de.icr.io/<replace_your_namespace/<replace_your_image_name>:${BUILD_ID} .'
            }
        }
        stage('Deploy') {
            git url: 'https://github.com/volaka/jenkins-nodejs-app.git'
            container('deploy') {
                sh 'ibmcloud login -a cloud.ibm.com -r eu-de --apikey ${IBMCLOUD_TOKEN}'
                sh 'ibmcloud ks cluster config --cluster <replace_your_cluster_name>'
                sh 'sed -i "s~^\\([[:blank:]]*\\)image:.*$~\\1image: de.icr.io/<replace_your_namespace>/<your_application_name>:${BUILD_ID}~" deployment.yml'
                sh 'kubectl apply -f deployment.yml -n default'
                sh 'kubectl get svc -n nodejs'
            }
        }
    }
}
