podTemplate(
    containers: [
        containerTemplate(name: 'jnlp', image: 'jenkins/inbound-agent:jdk17', args: '${computer.jnlpmac} ${computer.name}'),
        containerTemplate(name: 'docker', image: 'docker:26.1.3', command: 'cat', ttyEnabled: true)
    ],
    volumes: [
        hostPathVolume(hostPath: '/var/run/docker.sock', mountPath: '/var/run/docker.sock')
    ]
) 
{
  node(POD_LABEL) {
    stage('Checkout Code') {
      git branch: 'main', url: 'https://github.com/gearhub-1/simple-quote-app'
    }
    stage('Docker build') {
      container("docker"){
        sh "docker build -t $services:$tag -f ./$services/app.dockerfile ./$services"
      }
    }
  }
}