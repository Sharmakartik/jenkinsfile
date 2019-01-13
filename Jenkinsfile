pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                echo " build
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
   post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }  
}
