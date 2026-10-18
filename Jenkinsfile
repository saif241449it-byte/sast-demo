pipeline {
    agent any

    tools {
        jdk 'JDK25'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the source code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Maven project...'
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo 'Starting SonarQube analysis...'

                withSonarQubeEnv('SonarQube') {
                    bat 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:5.1.0.4751:sonar -Dsonar.projectKey=sast-Demo -Dsonar.projectName=SAST-Demo'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and SonarQube analysis completed successfully.'
        }

        failure {
            echo 'Build or analysis failed. Check the Console Output.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
