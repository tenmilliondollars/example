podTemplate {
    node(POD_LABEL) {
        stage('Stage check') {
            input message: 'Deploy?', ok: 'Yes!'
        }
    }
}
podTemplate(yaml: '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: docker
    image: docker:19.03.1-dind
    securityContext:
      privileged: true
    env:
      - name: DOCKER_TLS_CERTDIR
        value: ""
''') {
    node(POD_LABEL) {
        sh 'git clone https://github.com/tenmilliondollars/example.git --branch develop example'
        container('docker') {
            sh 'echo $(BRANCH_NAME)'
            sh 'docker build -t docker-example ./example'
        }
    }
}
