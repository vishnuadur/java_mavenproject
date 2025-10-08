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
        	sh 'mvn -B clean package -Dmaven.test.skip=true'
    		}
	}


        stage('Archive') {
            steps {
                // Archive the built WAR file
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }

		stage('Sonarqube Analysis') {
			steps {
				withSonarqubeEnv('Sonarqube') {
					sh 'sonar-scanner'
				}
			}
		}
    }
}
