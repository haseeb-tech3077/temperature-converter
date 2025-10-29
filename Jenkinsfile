pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }

    environment {
        STUDENT_NAME = 'Abdul Haseeb'
        VERSION = "1.0.${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/haseeb-tech3077/temperature-converter'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build') {
            steps {
                bat 'npm run build'
                bat 'if not exist build mkdir build'
                bat 'echo Version: %VERSION% > build\\version.txt'
            }
        }

        stage('Test') {
            steps {
                bat 'npm test'
            }
        }

        stage('Package') {
            steps {
                powershell 'Compress-Archive -Path build -DestinationPath build_${env:VERSION}.zip'
            }
        }

        stage('Deploy (Simulated)') {
            steps {
                echo "Deploying version ${VERSION} for ${STUDENT_NAME}..."
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            deleteDir()
        }
    }
}