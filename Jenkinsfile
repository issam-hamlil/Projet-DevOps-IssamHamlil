pipeline {
    agent {
        docker { 
            image 'python:3.12'
        }
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub...'
                sh 'ls -la'
            }
        }
        
        stage('Build & Test') {
            steps {
                echo 'Running Python Application...'
                sh 'python app.py' 
            }
        }
        
        stage('Archive') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: 'app.py, README.md', fingerprint: true
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            script {
                def slackUrl = 'https://hooks.slack.com/services/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' 
                def message = "✅ Succès du Build: ${env.JOB_NAME} #${env.BUILD_NUMBER}\nVoir: ${env.BUILD_URL}"
                
                sh "curl -X POST -H 'Content-type: application/json' --data '{\"text\":\"${message}\"}' ${slackUrl}"
            }
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
