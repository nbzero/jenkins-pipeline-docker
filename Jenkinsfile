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
    docker.withRegistry('https://172.17.0.2:5000') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
  }
  stage('Deploy on staging environment') {
    echo "Deploy with helm"
  }
}
