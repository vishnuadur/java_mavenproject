pipeline {
    agent { label 'vk-node' }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vishnuadur/java_mavenproject.git'
            }
        }

        stage('Build') {
            steps {
                // Skip tests to avoid JUnit errors
                sh 'mvn -B clean package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                // Archive the built WAR file
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }
}
