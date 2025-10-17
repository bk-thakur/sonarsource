pipeline {
    agent any

    tools {
        jdk 'jdk17'                 // Name of JDK configured in Jenkins Tools
        sonarQubeScanner 'sonar-scanner'  // Name of SonarQube Scanner in Jenkins Tools
    }

    environment {
        SONARQUBE = 'SonarQubeLocal'  // Name of your SonarQube server in Jenkins
        PROJECT_KEY = 'jenkins-test-project' // Unique project key
        PROJECT_NAME = 'Jenkins Test Project'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SonarSource/sonar-scanning-examples.git'
            }
        }

        stage('Build') {
            steps {
                echo "Build step placeholder (add actual build commands here)"
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeLocal') {
                    sh """
                        sonar-scanner \
                          -Dsonar.projectKey=${PROJECT_KEY} \
                          -Dsonar.projectName='${PROJECT_NAME}' \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.login=$SONAR_AUTH_TOKEN
                    """
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        success {
            echo "SonarQube analysis completed successfully!"
        }
        failure {
            echo "Build failed due to Quality Gate or other issues."
        }
    }
}

