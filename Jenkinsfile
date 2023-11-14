node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('181530151294.dkr.ecr.ap-northeast-2.amazonaws.com/ssung-test/', 'ecr-credential') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
