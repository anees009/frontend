pipeline {
    agent {
        label 'jenkins-slave'
    }
    stages {
        stage('Checkout') {
            steps {
                sh 'echo "Building..." '
                sh 'sleep 5'
                sh 'ls'
                sh 'echo "Sleep done"'
            }
        }
    }
}
