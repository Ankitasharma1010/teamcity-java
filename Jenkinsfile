pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube'  // This should match the name of your SonarQube server in Jenkins configuration
        // MAVEN_HOME = tool name: 'Maven 3', type: 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your project code from your repository
                git 'https://github.com/Ankitasharma1010/teamcity-java.git'
            }
        }

        stage('Build') {
            steps {
                // Build your project using Maven
                script {
                    sh "mvn clean package -DskipTests"
                }
            }
        }
       

        stage('SonarQube Analysis') {
            steps {
                def mvn = tool 'Default Maven';
                withSonarQubeEnv() {
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=Task -Dsonar.projectName='Task'"
                }
            }
        }
    }

    post {
        always {
            // Clean up or post actions (e.g., sending notifications)
            echo 'Cleaning up after the pipeline'
        }
    }
}
