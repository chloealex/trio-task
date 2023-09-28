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
    stage('Deploy Containers') {
      steps {
        sh '''
        ssh jenkins@chloe-appserver << EOF
        docker pull chloealex/mysql
        docker pull chloealex/flask-app
        docker pull chloealex/nginx
        docker network create trio
        docker volume create trio
        docker run -d -e MYSQL_ROOT_PASSWORD --network trio:/var/lib/mysql --name mysql chloealex/mysql
        docker run -d -e MYSQL_ROOT_PASSWORD --network trio --name flask-app chloealex/flask-app
        docker run -d -p 80:80 --network trio --name nginx chloealex/nginx
        '''
      }
  }
}

