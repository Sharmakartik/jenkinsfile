pipeline {
    agent {
        node {
        label 'windows'
    }
    }
    stages {
        stage('Build') { 
            steps {
                echo " build"
            }
        }
        stage('Test') { 
            steps {
                echo " Test"
            }
        }
        stage('Deploy') { 
            steps {
                echo " deploy"
            }
        }
    }
}
