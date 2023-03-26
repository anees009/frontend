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
                // Checkout the repository
                echo ${env.BRANCH_NAME}
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/dev']], 
                          userRemoteConfigs: [[url: 'https://github.com/anees009/frontend.git']]])
                
                // Run build steps only when a merge happens to the dev branch
                script {
                    withEnv(["BRANCH_NAME=${env.BRANCH_NAME}", "GITHUB_PULL_REQUEST_BRANCH=${env.GITHUB_PULL_REQUEST_BRANCH}"]) {
                        if ("${BRANCH_NAME}" == 'dev' && "${GITHUB_PULL_REQUEST_BRANCH}" == 'dev') {
                            sh 'date'
                            sh 'ls'
                            echo "Current branch name: ${BRANCH_NAME} and pull branch: ${GITHUB_PULL_REQUEST_BRANCH}"
                        } else {
                            echo "Skipping build steps as no merge happened to the dev branch"
                            echo "Current branch name: ${BRANCH_NAME} and pull branch: ${GITHUB_PULL_REQUEST_BRANCH}"
                        }
                    }
                }
            }
        }
    }
}
