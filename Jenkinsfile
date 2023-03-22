pipeline {
    agent any
    stages {
        stage('soanr quality status') {
            agent {
                docker {
                    image 'maven'
                }
            }
            stage('Maven build') {
                steps {
                    script {
                        sh 'mvn clean install'
                    }
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
