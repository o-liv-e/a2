pipeline {
    agent any
    
    parameters {
        booleanParam(name: 'SEND_EMAIL', defaultValue: true, description: 'Check to send an email notification after the build.')
    }
    
    environment {
        APP_NAME    = 'MyPythonApp'
        APP_VERSION = '1.2.0'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo "Compiling ${env.APP_NAME} v${env.APP_VERSION}..."
                bat 'python -m py_compile app.py'
            }
        }
        
        stage('Send Notification') {
            when {
                expression { params.SEND_EMAIL == true }
            }
            steps {
                echo "Notification:"
                echo "Subject: ${env.APP_NAME} v${env.APP_VERSION} - ${JOB_NAME} #${BUILD_NUMBER} completed"
                echo "Build URL: ${BUILD_URL}"
               }
        }
    }
}
