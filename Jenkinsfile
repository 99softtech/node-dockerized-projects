pipeline {
  agent any
  stages {    
    stage('checkout') {
      steps {
        checkout scm
      }
    }        
    stage('Install dependencies') {
      steps {
        sh 'npm install'
      }
    }     
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }             
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }  
  }
}
