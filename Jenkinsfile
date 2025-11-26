pipeline {
    agent any
 
    tools {
        nodejs "node16"
    }
 
    environment {
        // for private repositories
        GIT_CREDENTIALS = credentials('github-token')
    }
 
    stages {
 
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/yourusername/your-nodejs-repo.git'
            }
        }
 
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
