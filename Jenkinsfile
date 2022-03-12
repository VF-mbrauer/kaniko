podTemplate(yaml: """
kind: Pod
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    imagePullPolicy: Always
    command:
    - /busybox/cat
    tty: true
    volumeMounts:
      - name: kaniko-secret
        mountPath: /kaniko/.docker/
    resources: {}
  volumes:
    - name: kaniko-secret
      secret:
        secretName: regcred
        items:
          - key: .dockerconfigjson
            path: config.json
"""
  ) {
  node(POD_LABEL) {
    stage('GIT') {
      
    }
    
    stage('Building Image with Kaniko') {
      container('kaniko') {
          sh '/kaniko/executor -f `pwd`/Dockerfile -c `pwd` --context=git://github.com/VF-mbrauer/kaniko-demo --destination=maikbrauer/kaniko:1.0.0'
      }
    }
  }
}