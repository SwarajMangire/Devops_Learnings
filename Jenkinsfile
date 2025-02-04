pipeline {
    agent any  // Runs on any available agent

    environment {
        NODEJS_HOME = "/usr/local/bin"  // Update this if Node.js is installed in a different path
        PATH = "$NODEJS_HOME:$PATH"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'jenkins', url: 'https://github.com/SwarajMangire/Devops_Learnings.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'  // Installs Angular dependencies
                }
            }
        }

        stage('Build Angular App') {
            steps {
                script {
                    sh 'npm run build --prod'  // Builds the Angular app
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    sh 'npm test'  // Runs Angular unit tests
                }
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo 'Deploying Application...' 
                // Add deployment commands here if needed
            }
        }
    }

    post {
        success {
            echo 'Build successful! 🎉'
        }
        failure {
            echo 'Build failed! ❌'
        }
    }
}
