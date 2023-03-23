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
        post {
		always {
			mail bcc: '', body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", cc: '', charset: 'UTF-8', from: '', mimeType: 'text/html', replyTo: '', subject: "${currentBuild.result} CI: Project name -> ${env.JOB_NAME}", to: "taniaduggal60@gmail.com";  
		}
	}
    }
}
}
