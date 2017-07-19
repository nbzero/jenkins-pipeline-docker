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
    echo "Deploying with tag: " + version
    docker.withRegistry('https://172.17.0.2:5000') {
        app.push(version)
        app.push("latest")
    }
  }
  stage('Deploy on Staging environment') {
    echo "Deploying Staging with helm"
    // ...
    echo "Deployed"
  }
  stage('Deploy on UAT environment') {
    echo "Deploying UAT with helm"
    // ...
    echo "Deployed"
  }
  stage('Deploy on Production environment') {
    input "Ready for production?"
    echo "Deploying Production with helm"
    // ...
    echo "Deployed"
  }
}
