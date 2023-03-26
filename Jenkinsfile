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
                // Run build steps only when a merge happens to the dev branch
                script {
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
