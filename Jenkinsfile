pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool 'SonarQube Scanner'
        SONARQUBE_TOKEN = credentials('sonarqube-token') // Simpan token sebagai Secret Text di Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                url: 'https://github.com/mascoolin/jenkins-sonarqube.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh(script: "${SONAR_SCANNER_HOME}/bin/sonar-scanner -Dsonar.projectKey=myapp -Dsonar.sources=. -Dsonar.host.url=http://192.168.1.15:9000 -Dsonar.login=${SONARQUBE_TOKEN}", 
                    returnStdout: true)
                }
            }
        }
    }
}
