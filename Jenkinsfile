@Library('kartiklibrary') _

pipeline {
    agent any
    tools {
        maven 'maven'
    }
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
            tools {
                maven 'maven' 
               }
            steps {
               script {
                bat 'mvn -version'  
                echo " Test"
                   echo "using script block in steps{...}"   
               }
            }
        }
        stage('Deploy') { 
            when {
                branch 'master'
            }
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "kartik"
                parameters {
                    string(name: 'PERSON', defaultValue: 'kartik', description: 'Who should I say hello to?')
                }
              }  
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
       stage('shared-library') {
           steps {
               
             script { 
                h.cmmdd()
                utils.mvn 'clean package'
                
              }
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
            //emailnotify(currentBuild.currentResult)
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
