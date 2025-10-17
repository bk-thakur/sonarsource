pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clones a sample repo with code
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
