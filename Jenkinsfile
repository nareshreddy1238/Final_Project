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
                echo 'Unit Testing....'
                sh 'mvn test'
            }
        post {
         always {
           junit '**/target/surefire-reports/*.xml'
           step([$class: 'CoberturaPublisher', autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/coverage.xml', failUnhealthy: false, failUnstable: false, maxNumberOfBuilds: 0, onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false])
              }
             }
           }
 
  }
 }
    
