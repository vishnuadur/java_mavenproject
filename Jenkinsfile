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
                sh 'mvn -B clean package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                WAR_FILE=$(ls target/*.war | head -n 1)
                echo "Deploying $WAR_FILE to Tomcat..."
                scp -o StrictHostKeyChecking=no $WAR_FILE ubuntu@<TOMCAT_SERVER_IP>:/opt/tomcat/webapps/
                '''
            }
        }
    }
}
