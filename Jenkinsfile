pipeline {
    agent any
    stages {
        stage('soanr quality status') {
            agent {
                docker {
                    image 'maven'
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
                    withSonarQubeEnv(credentialsId: 'sonar-token1')
                    }
                }
            }
        }
    }
}
