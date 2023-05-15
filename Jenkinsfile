pipeline {
    agent any
    
    tools {
        maven 'maven-3.9.1'
    }

    stages {
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Sonar Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
