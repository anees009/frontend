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
                checkout([$class: 'GitSCM', 
                          branches: [[name: '*/dev']], 
                          userRemoteConfigs: [[url: 'https://github.com/anees009/frontend.git']]])
                
                // Run build steps only when a merge happens to the dev branch
                script {
                    withEnv(["BRANCH_NAME=${env.BRANCH_NAME}"]) {
                        if (env.BRANCH_NAME == 'dev' && env.GITHUB_PULL_REQUEST_BRANCH == 'dev') {
                            sh 'date'
                            sh 'ls'
                            echo "Current branch name: ${env.BRANCH_NAME} and pull branch: ${env.GITHUB_PULL_REQUEST_BRANCH}"
                        } else {
                            echo "Skipping build steps as no merge happened to the dev branch"
                            echo "Current branch name: ${env.BRANCH_NAME} and pull branch: ${env.GITHUB_PULL_REQUEST_BRANCH}"
                        }
                    }
                }
            }
        }
    }
}
