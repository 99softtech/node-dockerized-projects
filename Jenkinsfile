pipeline {
  agent any
  environment {
        PATH = "/usr/local/bin:$PATH"  // Adjust based on where Docker is installed
        DOCKER_CREDENTIALS_ID = '273063cb-a644-4769-a880-02bab10feccc'  // Replace with your Docker credentials ID in Jenkins
        IMAGE_NAME = '99softtech/my-node-app'  // Replace with your Docker Hub username and image name
        IMAGE_TAG = 'latest'  // Or dynamically set this with git commit, date, or other variables
 
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
          withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
            sh '''
              echo $DOCKERHUB_PASSWORD | docker login -u $DOCKERHUB_USERNAME --password-stdin
            '''
          }
        }
      }
    }
  }
}
