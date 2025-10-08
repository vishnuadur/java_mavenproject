pipeline {
    agent { label 'vk-node' }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/vishnuadur/java_mavenproject.git', 
                    credentialsId: '93b94bea-507f-404e-9d4c-9ed8ef531cb1'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -B clean package -Dmaven.test.skip=true'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Replace 'YourSonarQubeName' with your actual SonarQube server name
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=demo1'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    // Fails the pipeline if Quality Gate fails
                    waitForQualityGate abortPipeline: true
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
