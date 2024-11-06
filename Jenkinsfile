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
        bat 'C:\Users\sunder.sharma\Downloads\PSTools\PsExec.exe -u 99softtech -p Aw3#se4$dr "docker build -t my-node-app:1.0 ."'
      }
    }
  }
}
