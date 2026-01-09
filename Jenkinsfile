pipeline {
    agent {
        docker { 
            image 'python:3.9-slim' 
            args '-u -p 3000:3000' // Arguments needed for docker to run smoothly
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Jenkins automatically checks out the code from SCM (GitHub)
                echo 'Checking out code from GitHub...'
                sh 'ls -la' // Verifies the files are there
            }
        }

        stage('Build & Test') {
            steps {
                echo 'Running Python Application...'
                // Requirement: "test et exécute votre application"
                sh 'python app.py' 
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving artifacts...'
                // Requirement: "archiver votre projet"
                archiveArtifacts artifacts: 'app.py, README.md', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
             // Requirement: "Notify Slack"
             // Note: You need the Slack plugin installed in Jenkins for this to work
             // slackSend channel: '#devops', message: "Succès du Pipeline: ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
             echo 'Slack notification would be sent here (Plugin required)'
        }
        failure {
             echo 'Pipeline failed.'
        }
    }
}