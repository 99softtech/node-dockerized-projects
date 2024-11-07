pipeline {
  agent any
  environment {
        PATH = "/usr/local/bin:$PATH"  // Adjust based on where Docker is installed
   }
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
    stage('Login to Docker Hub') {
      steps {
        script {
          // Login to Docker Hub using Jenkins credentials
          withCredentials([usernamePassword(credentialsId: 'docker-cred', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
            sh 'echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin'
            sh 'docker tag my-node-app:1.0 99softtech/my-node-app:1.0'
            sh 'docker push 99softtech/my-node-app:1.0'
            sh 'docker logout'
          }
        }
      }
    }
  }
}
