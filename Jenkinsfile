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
     stage('Run') {
      steps {
        sh 'docker run -d --name mysql chloealex/mysql:latest'
        sh 'docker run -d --name flask-app chloealex/flask-app:latest'
        sh 'docker run -d -p 80:80 --name nginx chloealex/nginx:latest'
      }
    }

  }
}

