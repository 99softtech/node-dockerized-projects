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
       sh '''
        export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"
        brew install npm
        npm install
        '''
      }
    }     
    stage('Test') {
      steps {
        sh '''
         export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"
         npm test
         '''
      }
    }             
    stage('Build') {
      steps {
        sh '''
         export PATH="/opt/homebrew/bin:/usr/local/bin:$PATH"
         npm run build
         '''
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
