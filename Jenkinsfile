pipeline {
    agent any

    tools {
        jdk 'jdk17'   // Name must match the JDK configured in Jenkins Tools
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SonarSource/sonar-scanning-examples.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeLocal') {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=test-project \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=http://localhost:9000 \
                          -Dsonar.login=$SONAR_AUTH_TOKEN
                    '''
                }
            }
        }
    }
}
