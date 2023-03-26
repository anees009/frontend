pipeline {
    agent {
        label 'jenkins-kaniko'
    }
    triggers {
        githubPush()
    }
    environment {
        REGISTRY_URL = "us.icr.io" // Update with your IBM Cloud Container Registry URL
        IMAGE_NAME = "anees_test/frontend-img"
        IMAGE_TAG = "25"
        DOCKER_CONFIG = credentials('my-docker-config') // Jenkins credentials with Docker config.json file
        PATH = "$PATH:/busybox:/kaniko/"
    }
    stages {
        stage('Build docker image') {
            steps {
                container('builder') {
                    sh "executor --context `pwd` --dockerfile `pwd`/Dockerfile --destination ${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}
