node {
  def app
  stage('Checkout project repository'){
    checkout scm
  }
  stage('Build project docker image'){
    app = docker.build("kpc")
  }
  stage('Test project image'){
    sh "docker run kpc"
  }
  stage('Push project image'){
    def version = input(id: 'version', message: 'Please input version tag', parameters: [
    [$class: 'TextParameterDefinition', defaultValue: "${env.BUILD_NUMBER}", \
      description: 'Versioning input', name: 'version']
    ])
    echo "Deploying with " + version
    docker.withRegistry('https://172.17.0.2:5000') {
        app.push(version)
        app.push("latest")
    }
  }
  stage('Deploy on staging environment') {
    echo "Deploy with helm"
  }
}
