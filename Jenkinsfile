// pipeline{
//     agent any
//
//     tools{
//         maven "maven"
//         jdk "JDK17"
//     }
//
//     stages{
//
//         stage("Sourcode Checkout"){
//             steps{
//                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/SurajPatil-SP/jenkins-ci-cd.git']])
//             }
//         }
//
//         stage("Build Process"){
//             steps{
//                 script{
//                     bat 'mvn clean install'
//                 }
//             }
//         }
//
//         stage("Deploy to Container"){
//             steps{
//                 deploy adapters: [tomcat8(credentialsId: 'Tomcat-Password', path: '', url: 'http://localhost:8081/')], contextPath: 'jenkinsCiCd', war: '**/*.war'
//             }
//         }
//
//     }
//
//     post(){
//         always{
//             emailext attachLog: true, body: '''<html>
//    <body>
//    <p>Build Status: ${BUILD_STATUS}</p>
//    <p>Build Number: ${BUILD_NUMBER}</p>
//    <p>Check the <a href="${BUILD_URL}">console output</a></p>
//    </body>
// </html>''', mimeType: 'text/html', replyTo: 'surajbpatil6116@gmail.com', subject: 'Pipeline Status : ${BUILD_STATUS}  #${BUILD_NUMBER}', to: 'surajbpatil6116@gmail.com'
//         }
//     }
// }