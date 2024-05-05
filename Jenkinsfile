pipeline {
    agent {label 'master'}
    tools{
        jdk 'jdk17'
        maven 'maven'
    }
    environment {
        CHEIF_AUTHOR = 'Asher'
        RETRY_CNT = 3
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '3')) 
        disableConcurrentBuilds()
        quietPeriod(5)
    }
    parameters {
     choice(name: 'TARGET_ENV', choices: ['UAT', 'SIT', 'STAGING'], description: 'Pick something')
    }
 
    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
                sh "echo $CHEIF_AUTHOR"
            }
        }
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
         stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
         stage('Package') {
            steps {
                sh 'mvn package'
                sh 'echo done'
            }
        }
        
    }
    post {
        always {
            emailext attachLog: true, body: 'Hello ', subject: "BUIILD STATAUS $JOB_NAME", to: 'mukunjshop@gmail.com, atin@pragra.io'
        }
        success {
            mail  body: 'Hello from Jenkins', from: 'jenkins@pragra.io', subject: 'BUIILD SUCCESS FULL $JOB_NAME', to: mukunjshop@gmail.com'
        }
    }
}
