pipeline {
    agent {
        docker { image 'node:7-alpine' }
    }
    environment {
        PATH = "$PATH:/usr/local/bin"
    }
    stages {
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
}