pipeline {
    agent {
        label 'jenkins-kaniko'
    }
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                echo "${env.GITHUB_PULL_REQUEST_BRANCH}"
                // Run build steps only when a merge happens to the dev branch
                script {
                    withEnv(["BRANCH_NAME=${env.GIT_BRANCH}"]) {
                        if ("${BRANCH_NAME}" == 'origin/dev') {
                            sh 'date'
                            sh 'ls'
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
                script {
                    sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --destination=anees_test/frontend-img:25"
                }
            }
        }
    }
}
