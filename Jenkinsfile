pipeline {
    agent {
        label 'jenkins-slave'
    }
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout') {
            steps {
                echo "${env.GIT_BRANCH}"
                // Run build steps only when a merge happens to the dev-branch
                script {
                    withEnv(["BRANCH_NAME=${env.GIT_BRANCH}"]) {
                        if ("${BRANCH_NAME}" == 'origin/dev') {
                            sh 'date'
                            sh 'ls'
                            echo "Current branch name: ${BRANCH_NAME}"
                        } else {
                            echo "Skipping build steps as no merge happened to the dev branch"
                            echo "Current branch name: ${BRANCH_NAME} "
                        }
                    }
                }
            }
        }
    }
}
