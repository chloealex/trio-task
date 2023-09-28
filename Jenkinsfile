pipeline {

    agent any

  stages {
    stage('Build') {
      steps {
        sh 'docker build -t chloealex/mysql:latest ./db'
        sh 'docker build -t chloealex/flask-app:latest ./flask-app'
        sh 'docker build -t chloealex/nginx:latest ./nginx'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push chloealex/mysql'
        sh 'docker push chloealex/flask-app'
        sh 'docker push chloealex/nginx'
      }
    }
  }
}

