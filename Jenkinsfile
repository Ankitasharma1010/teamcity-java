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
                git ''
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
                script {
                    // Run SonarQube analysis using the Maven plugin
                    sh "'${MAVEN_HOME}/bin/mvn' sonar:sonar -Dsonar.projectKey=hello-world -Dsonar.host.url=http://localhost:9000 -Dsonar.login=YOUR_SONARQUBE_TOKEN"
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
