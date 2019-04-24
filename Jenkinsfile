pipeline {
  agent {
    docker {
      image 'node:7-alpine'
    }

  }
  stages {
    stage('Install docker-compose') {
      steps {
        sh 'curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose'
        sh 'sudo chmod +x /usr/local/bin/docker-compose'
      }
    }
    stage('Build') {
      steps {
        sh 'docker-compose build'
      }
    }
    stage('Setup Database') {
      steps {
        sh 'docker-compose run app rake db:create'
        sh 'docker-compose run app rake db:migrate'
      }
    }
    stage('Test') {
      steps {
        sh 'docker-compose run app rake test'
      }
    }
  }
  environment {
    PATH = "$PATH:/usr/local/bin"
  }
}