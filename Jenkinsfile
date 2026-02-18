pipeline {
    agent any

    tools {
        maven 'Maven3'     // Jenkins → Global Tool Configuration
        jdk 'JDK11'
    }

    environment {
        SONAR_SCANNER_HOME = tool 'SonarScanner'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-org/your-repo.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh """
                    mvn sonar:sonar \
                    -Dsonar.projectKey=rahul01-key_rahultrend \
                    -Dsonar.projectName=rahultrend \
                    -Dsonar.organization=rahul01-key
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully 🎉'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}

