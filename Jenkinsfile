node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("181530151294.dkr.ecr.ap-northeast-2.amazonaws.com/ssung-test")
         
     }
     stage('Push image') {
         docker.withRegistry('https://181530151294.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:ecr-credential') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }

     stage('K8S Manifest Update') {
        steps {
            git credentialsId: 'gitops_token',
                url: 'https://github.com/sssungyoung/flask-example-apps.git',
                branch: 'main'

            sh "sed -i 's/ssung-test:.*\$/ssung-test:${currentBuild.number}/g' flask-example-deploy/deployment.yaml"
            sh "git add deployment.yaml"
            sh "git commit -m '[UPDATE] my-app ${currentBuild.number} image versioning'"
            sshagent(credentials: ['{k8s-manifest repository credential ID}']) {
                sh "git remote set-url origin git@github.com/sssungyoung/flask-example-apps.git"
                sh "git push -u origin main"
             }
        }
        post {
                failure {
                  echo 'K8S Manifest Update failure !'
                }
                success {
                  echo 'K8S Manifest Update success !'
                }
        }
    }
}
