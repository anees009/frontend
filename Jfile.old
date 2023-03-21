pipeline {
    agent {
        label "jenkins-docker"
    }
    environment {
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Build docker image') {
            steps {
                script {
                    IMAGE_TAG = sh(returnStdout: true, script: 'git log -n1 --format="%h"').trim()
                }
                sh "docker build --build-arg IMAGE_TAG=${IMAGE_TAG} -t frontend:${IMAGE_TAG} ."
            }
        }
        stage('List docker image') {
            steps {
                sh 'docker images'
            }
        }
    }
}

