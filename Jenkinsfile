pipeline {
    agent { label 'vk-node' }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/vishnuadur/java_mavenproject.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn -B test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'  // test results in Jenkins
        }
    }
}
