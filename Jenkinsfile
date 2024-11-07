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
    // stage('Check Docker') {
    //   steps {
    //     sh 'docker --version'
    //   }
    // }
    // stage('Build Image') {
    //   steps {
    //     sh 'docker build -t my-node-app:1.0 .'
    //   }
    // }
  }
}
