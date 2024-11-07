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
    stage('Check Docker') {
      steps {
        bat 'docker --version'  // Ensure Docker is accessible in the Jenkins environment
      }
    }
    stage('Build Image') {
      steps {
        // Run Docker build using PsExec to avoid password prompt
      // bat '"C:/Program Files/Docker/Docker/resources/bin/docker.exe" build -t my-node-app:1.0 .'
        bat '"C:/PSTools/PsExec.exe" -h "C:/Program Files/Docker/Docker/resources/bin/docker.exe" build -t my-node-app:1.0 .'
      }
    }
  }
}
