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
        }
        post {
         always {
          junit '**/target/surefire-reports/*.xml'
    }
  }
 }
}
    
