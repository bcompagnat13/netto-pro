pipeline {
    agent any
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