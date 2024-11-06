pipeline {
  agent any

  tools {nodejs "node"}

  stages {    
    stage('Cloning Git') {
      steps {
        git 'https://github.com/99softtech/node-dockerized-projects.git'
      }
    }        
    stage('Install dependencies') {
      steps {
        sh 'npm i -save express'
      }
    }     
    stage('Test') {
      steps {
         sh 'node index.js'
      }
    }             
  }
}
