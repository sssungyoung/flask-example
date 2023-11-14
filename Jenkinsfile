node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build()
         
     }
     stage('Push image') {
         docker.withRegistry('https://181530151294.dkr.ecr.ap-northeast-2.amazonaws.com/ssung-test', 'ecr:ap-northeast-2:ecr-credential') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
