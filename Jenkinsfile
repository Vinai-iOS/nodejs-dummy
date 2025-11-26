pipeline {
    agent any
 
    tools {
        nodejs "node16"
    }
 
    // environment {
    //     // for private repositories
    //     GIT_CREDENTIALS = credentials('github-token')
    // }
 
    stages {
 
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/Vinai-iOS/nodejs-dummy.git'
            }
        }
 
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
stage('Lint') {
            steps {
                sh 'npm run lint || true'
            }
        }
 
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
 
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
 
        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'dist/**/*.*', fingerprint: true
            }
        }
 
        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying to production server..."
 
                // Example deployment command
                sh '''
                ssh -o StrictHostKeyChecking=no ubuntu@YOUR_SERVER_IP "cd /var/www/app && git pull && pm2 restart all"
                '''
            }
        }
    }
 
    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
