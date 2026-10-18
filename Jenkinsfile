pipeline {
    agent any

    tools {
        jdk 'JDK25'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the source code...'
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
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar -Dsonar.projectKey=sast-demo -Dsonar.projectName=SAST-Demo'
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
    }
}
