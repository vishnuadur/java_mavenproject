pipeline {
    agent { label 'vk-agent' }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/<your-username>/java-jenkins-demo.git', branch: 'main'
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
