pipeline {
    agent any
    environment{
        VERSION = "${env.BUILD_ID}"
    }
    stages {
        stage('sonar quality status') {
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
        }
        stage('docker build and docker push to nexus repo'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'nexus_passwd', variable: 'nexus-creds')]) {
                    sh '''
                      docker build -t 54.165.20.131:8083/springapp:${VERSION} .
                      docker login -u admin -p nexus 54.165.20.131:8083
                      docker push 54.165.20.131:8083/springapp:${VERSION}
                      docker rmi 54.165.20.131:8083/springapp:${VERSION}
                    '''
                    }
                }
            }
        }
    }
}
