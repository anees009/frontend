pipeline {
    agent {
        label 'jenkins-slave'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/anees009/frontend.git']]])
                sh 'echo "Building..." '
                sh 'sleep 5'
                sh 'echo "Sleep done"'
            }
        }
    }
}
