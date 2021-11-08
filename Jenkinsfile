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

        stage('Analysis') {
            steps {
                echo 'Sonar Analysis'
                sh 'mvn sonar:sonar -Dsonar.host.url=http://18.212.192.181:9000 -Dsonar.login=92d44bab121d10b467eb51e047167c057921df9b'
            }
         }
        
        stage('Publish'){
            steps {
                 echo 'Nexus Release'
                 sh 'mvn deploy'
               }
             post{
               always{
                 nexusArtifactUploader artifacts: [
                              [ 
                                artifactId: 'WebAppCal', 
                                classifier: '', 
                                file: 'target/WebAppCal-1.2.8.war', 
                                type: 'war'
                              ]
                          ], 
                          credentialsId: 'Nexus', 
                          groupId: 'com.web.cal', 
                          nexusUrl: '18.212.192.181:8081', 
                          nexusVersion: 'nexus2', 
                          protocol: 'http', 
                          repository: 'releases', 
                          version: '1.2.8'
             }
         }
      }
      stage('Deploy') {
            steps {
                sshagent(['Tomcat_user']) {
                sh 'scp -o StrictHostKeyChecking=no target/WebAppCal-1.2.8.war centos@172.31.80.138:~/apache-tomcat-7.0.94/webapps'
       }
      }
     }       
   }
 }
    
