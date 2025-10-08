pipeline {
    agent { label 'vk-node' }

    environment {
        SONAR_TOKEN = credentials('sqa_a0c9a372b25c19d129204d39d8722b9cab61e97d') // Your Jenkins SonarQube token credential ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vishnuadur/java_mavenproject.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean package -Dmaven.test.skip=true'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }

        stage('SonarQube Analysis') {
            steps {
                sh """
                    sonar-scanner \
                        -Dsonar.projectKey=demo1 \   # Replace with your Sonar project key
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://3.91.84.188:9000/ # Replace with your SonarQube server URL
                        -Dsonar.login=${SONAR_TOKEN}
                """
            }
        }
    }
}
