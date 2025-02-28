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
                        -Dsonar.host.url=http://<SONARQUBE_SERVER_IP>:9000 \
                        -Dsonar.login=<SONARQUBE_TOKEN>
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
