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
        bat 'npm install'
      }
    }     
    stage('Test') {
      steps {
        bat 'npm test'
      }
    }             
    stage('Build') {
      steps {
        bat 'npm run build'
      }
    }
    stage('Build Image') {
      steps {
        bat 'runas /user:Administrator "docker build -t my-node-app:1.0 ."'
      }
    }
  }
}
