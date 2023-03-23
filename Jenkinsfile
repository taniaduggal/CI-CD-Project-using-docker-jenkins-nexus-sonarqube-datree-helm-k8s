pipeline {
    agent any
    stages {
        stage('sonar quality status') {
            agent {
                docker {
                    image 'maven'
                }
            }
        }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token1') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        stage('quality gate checks') {
            steps {
                script {
                   waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token1'
                    }
                }
            }
    }
}
