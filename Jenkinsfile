pipeline {
    agent any
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
        stage('Run Tests'){
                 parallel {
                      stage('windows') {
                         steps {
                        echo "windows parallel"
                          }
                        }
                     stage('linux') {
                         steps {
                             echo "linux parallel"
                             }
                           }
                      }
        }
    }
}
