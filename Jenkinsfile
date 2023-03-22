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
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}
