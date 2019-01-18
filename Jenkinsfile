pipeline {
    agent any
     triggers {
        cron('H */4 * * 1-2')
    }
    environment { 
        CC = 'kartik'
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    options {
        timeout(time: 1000, unit: 'SECONDS') 
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
        stage('ENV'){
            steps{
                echo "hi from entier pipeline ${CC}"  
              
                }
              }
        stage('ENV--per-stage'){
            environment { 
                  CC = 'kartik-env-per-stage'
                }
            options {
                timeout(time: 100, unit: 'SECONDS') 
            }
            steps{
                echo "hi from entier pipeline ${CC}"  
              
                }
              }
        stage('Parameter-stage') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
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
