pipeline {
    agent any

    tools {
        jdk 'jdk17'                     // Must match JDK name in Jenkins
        sonarQubeScanner 'sonar-scanner' // Must match Sonar Scanner name in Jenkins
    }

    environment {
        SONARQUBE_ENV = 'SonarQubeLocal' // Must match the name in "Manage Jenkins → System → SonarQube Servers"
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
