pipeline {
    agent any

    environment {
        NODE_VERSION = '18'
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
                        sh '''
                        sudo dnf module reset nodejs -y
                        sudo dnf module enable nodejs:18 -y
                        sudo dnf install -y nodejs
                        '''
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
                sh 'npm run build --configuration=production'
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
                script {
                    def deployDir = '/var/www/html/'
                    sh "sudo mkdir -p ${deployDir}"
                    sh "sudo rm -rf ${deployDir}*"
                    sh "sudo cp -r dist/* ${deployDir}"
                    sh "sudo chown -R ec2-user:ec2-user ${deployDir}"
                }
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
