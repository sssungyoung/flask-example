node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("ssung/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://ec2-3-37-129-200.ap-northeast-2.compute.amazonaws.com/', 'docker-reg') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
