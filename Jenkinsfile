pipeline {
    agent any

    tools {
        sonarScanner 'SonarScanner'  // Sesuai dengan nama yang dikonfigurasi di Jenkins
    }

    environment {
        SONAR_HOST_URL = 'http://localhost:9000'  // Sesuaikan dengan URL SonarQube
        SONAR_TOKEN = credentials('sonarqube-token')  // Buat "sonarqube-token" di Jenkins
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
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey=jenkins-sonarqube \
                          -Dsonar.sources=. \
                          -Dsonar.host.url=$SONAR_HOST_URL \
                          -Dsonar.login=$SONAR_TOKEN
                    '''
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
