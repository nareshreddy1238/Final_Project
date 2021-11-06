pipeline {
    agent any

    stages {
        stage('validate') {
            steps {
                echo 'validate..'
                sh 'mvn compile'
            }
        }

        stage('Build') {
            steps {
                echo 'Building'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Unit Testing'
                sh 'mvn test'
            }
        post {
         always {
           junit '**/target/surefire-reports/*.xml'
               }
             }
           }
        
        stage('Code Covarage') {
             steps {
                 echo 'Code Covarage'
                 sh 'mvn cobertura:cobertura -Dcobertura.report.format=xml'
            }
         post {
           always{
             cobertura coberturaReportFile: '**/target/site/cobertura/coverage.xml'
            } 
          }
        }
  }
 }
    
