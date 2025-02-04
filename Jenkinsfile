pipeline {
    agent any

    environment {
        NODE_VERSION = '18' // Set Node.js version
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'your-credentials-id', url: 'https://github.com/SwarajMangire/Devops_Learnings.git'
            }
        }

        stage('Setup Node.js') {
            steps {
                script {
                    def nodeInstalled = sh(script: "node -v", returnStatus: true)
                    if (nodeInstalled != 0) {
                        sh 'curl -fsSL https://rpm.nodesource.com/setup_18.x | sudo bash -'
                        sh 'sudo yum install -y nodejs'
                    }
                    sh 'node -v'
                    sh 'npm -v'
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Angular App') {
            steps {
                sh 'npm run build --prod'
            }
        }

        stage('Archive Build Artifacts') {
            steps {
                archiveArtifacts artifacts: 'dist/**/*', fingerprint: true
            }
        }

        stage('Deploy (Optional)') {
            when {
                branch 'main'
            }
            steps {
                sh 'cp -r dist/* /var/www/html/' // Change destination as needed
            }
        }
    }

    post {
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build Failed. Check logs!'
        }
    }
}
