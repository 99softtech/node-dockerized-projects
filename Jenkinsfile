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
        // Install Homebrew if it’s not already installed
        sh '''
            if ! command -v brew &> /dev/null; then
                echo "Installing Homebrew..."
                /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
            else
                echo "Homebrew already installed"
            fi
        '''
        
        // Install npm using Homebrew
        sh '''
            if ! command -v npm &> /dev/null; then
                echo "Installing npm..."
                brew install npm
            else
                echo "npm is already installed"
            fi
        '''
        
        // Install project dependencies
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
