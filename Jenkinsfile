node {
  def app
  stage('clone repo'){
    // checkout scm
    echo "checkout scm"
  }
  stage('Build docker image'){
    app = docker.build("172.17.0.3:5000/kpc")
  }
  stage('Test image'){
    echo "test image"
  }
  stage('Push image'){
    docker.withRegistry('172.17.0.3:5000') {
        app.push("${env.BUILD_NUMBER}")
        app.push("latest")
    }
  }
}
