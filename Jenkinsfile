pipeline {
    agent {
        label 'jenkins-kaniko'
    }
    triggers {
        githubPush()
    }
    environment {
        REGISTRY_URL = "us.icr.io" // Update with your IBM Cloud Container Registry URL
        IMAGE_NAME = "frontend-img"
        IMAGE_TAG = "25"
        DOCKER_CONFIG = credentials('my-docker-config') // Jenkins credentials with Docker config.json file
        PATH = "$PATH:/busybox:/kaniko/"
    }
    stages {
        stage('Checkout') {
            steps {
                echo "${env.GITHUB_PULL_REQUEST_BRANCH}"
                // Run build steps only when a merge happens to the dev branch
                script {
                    withEnv(["BRANCH_NAME=${env.GIT_BRANCH}"]) {
                        if ("${BRANCH_NAME}" == 'origin/dev') {
                            echo "Current branch name: ${BRANCH_NAME}"
                        } else {
                            echo "Skipping build steps as no merge happened to the dev-branch"
                            echo "Current branch name: ${BRANCH_NAME} "
                        }
                    }
                }
            }
        }
        stage('Build docker image') {
            steps {
                container('builder') {
                    sh "executor --context `pwd` --dockerfile `pwd`/Dockerfile --destination ${REGISTRY_URL}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
    }
}
