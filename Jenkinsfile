pipeline {
    agent {
        label "jenkins-docker"
    }

    stages {
        stage('build docker image1') {
            steps {
                sh 'date'
            }
        }
        stage('build docker image2') {
            steps {
                sh 'date -u'
            }
        }
    }
}
