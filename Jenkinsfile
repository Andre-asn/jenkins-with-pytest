pipeline {
    agent any
    
    stages {
        stage('Install dependencies') {
            steps {
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }
        
        stage('Run tests') {
            steps {
                sh './venv/bin/pytest --junitxml=report.xml --cov=. --cov-report=html'
            }
        }
        
        stage('Publish Report') {
            steps {
                junit 'report.xml'
            }
        }
    }

    post {
        failure {
            mail to: 'asantiag1@stevens.edu',
                subject: "Failed Pipeline ${currentBuild.fullDisplayName}"
                body: "Build failed. Check ${env.BUILD_URL}"
        }
    }
}