node('jenkins-slave') {
  stage('Checkout and set agent'){
     checkout scm
  } 
}

pipeline {
    agent {
        label "jenkins-docker"
    }

    stages {
        stage('build docker image') {
            steps {
                sh 'date'
            }
        }
    }
}
