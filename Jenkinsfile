pipeline {
  agent any
  
  stages {
    stage('Install Dependencies') {
      steps {
        script {
          sh 'npm install'
        }
      }
    }
    
    stage('Build') {
      steps {
        script {
          sh 'npm run build --prod'
        }
      }
    }
    
    stage('Test') {
      steps {
        script {
          sh 'npm test'
        }
      }
    }
    
    stage('Deploy') {
      steps {
        script {
          // Deployment commands go here
        }
      }
    }
  }
}
