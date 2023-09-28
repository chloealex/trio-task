pipeline {

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t mysql:latest ./db'
        sh 'docker build -t flask-app:latest ./flask-app'
        sh 'docker build -t nginx:latest ./nginx'
      }
    }
    stage('Login') {
      steps {
        sh 'docker login -u chloealex -p Divariva1999'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push mysql'
        sh 'docker push flask-app'
        sh 'docker push nginx'
      }
    }
  }
  post {
    success {
      sh 'docker logout'
    }
  }
}
