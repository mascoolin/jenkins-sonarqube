pipeline {
    agent any

    environment {
        SONAR_SCANNER_HOME = tool 'SonarQube Scanner'
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
                    sh """
                        ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                        -Dsonar.projectKey=myapp \
                        -Dsonar.projectName=myapp \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=192.168.1.15:9000 \
                        -Dsonar.login=sqa_230e79717b9c28963da3d8d5d801e36aa3e3291e
                    """
                }
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean package' // Contoh untuk Java/Maven
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Deploy aplikasi ke server..."'
                // Tambahkan perintah deploy sesuai kebutuhan (e.g., SSH, Docker, dll.)
            }
        }
    }
}
