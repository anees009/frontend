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
                sh 'echo "Building..." '
                sh 'sleep 5'
                sh 'echo "Sleep done"'
                // Run build steps only when a merge happens to the master branch
                script {
                    if (env.BRANCH_NAME == 'dev' && env.GITHUB_PULL_REQUEST_BRANCH == 'dev') {
                        sh 'date'
                        sh 'ls'
                    } else {
                        echo "Skipping build steps as no merge happened to the master branch"
                    }
                }
                
            }
        }
    }
}
