pipeline {
    agent any

    tools {
        sonarQube 'SonarScanner'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mascoolin/jenkins-sonarqube.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'sonar-scanner -Dsonar.projectKey=MyProject -Dsonar.sources=.'
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
}
