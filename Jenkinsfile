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
