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
        sh '/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"'
        sh 'brew install npm'
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
    stage('Check Docker') {
      steps {
        sh 'docker --version'
      }
    }
    stage('Build Image') {
      steps {
        sh 'docker build -t my-node-app:1.0 .'
      }
    }
  }
}
