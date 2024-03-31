pipeline{
    agent any

    tools{
        maven "maven"
        jdk "JDK17"
    }

    environment{
        APP_NAME = "spring-docker-cicd"
        RELEASE_NO = "1.0"
        DOCKER_USER = "surajbpatil"
        IMAGE_NAME = "${DOCKER_USER}"+"/"+"${APP_NAME}"
        IMAGE_TAG = "${RELEASE_NO}-${BUILD_NUMBER}"
    }

    stages{

        stage("Sourcode Checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SurajPatil-SP/jenkins-ci-cd.git']])
            }
        }

        stage("Build Process"){
            steps{
                script{
                    bat 'mvn clean install'
                }
            }
        }

        stage("Build Image") {
            steps{
                script{
                    bat 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
                }
            }
        }

        stage("Deploy Image to Hub") {
            steps{
                withCredentials([string(credentialsId: 'docker-cred', variable: 'docker-cred')]) {
                    echo 'docker login -u surajbpatil -p %docker-cred%'
                    bat 'docker login -u surajbpatil -p %docker-cred%'
                    bat 'docker push ${IMAGE_NAME}:${IMAGE_TAG}'
                }
            }
        }

    }

    post(){
        always{
            emailext attachLog: true, body: '''<html>
   <body>
   <p>Build Status: ${BUILD_STATUS}</p>
   <p>Build Number: ${BUILD_NUMBER}</p>
   <p>Check the <a href="${BUILD_URL}">console output</a></p>
   </body>
</html>''', mimeType: 'text/html', replyTo: 'surajbpatil6116@gmail.com', subject: 'Pipeline Status : ${BUILD_STATUS}  #${BUILD_NUMBER}', to: 'surajbpatil6116@gmail.com'
        }
    }
}