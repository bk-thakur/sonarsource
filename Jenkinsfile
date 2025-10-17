pipeline {
    agent any

    tools {
        jdk 'jdk17'
        sonarQubeScanner 'sonar-scanner'
    }

    environment {
        SONARQUBE_ENV = 'SonarQubeLocal'  // must match name in Manage Jenkins → System → SonarQube Servers
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/bk-thakur/sonarsource.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=local-freestyle \
                          -Dsonar.sources=. \
                          -Dsonar.projectBaseDir=${WORKSPACE}
                    '''
                }
            }
        }
    }
}
