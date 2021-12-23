pipeline {
    agent any
    triggers {
        githubPush()
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: "10"))
    }
    stages {
        stage('Build') {
          when{ branch 'main' }
          agent{
                  docker {
                      image 'maven'
                      args '--user 0:0'
                  }
          }
          steps {
                
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'b2fba6f9-e9e7-4198-9ac7-8c3d8a4a4645', keyFileVariable: 'SSH_KEY')]) {
                    sh 'cd /home/ubuntu/latest/BootStrapTomcat/target/' }
sh “docker-compose up -d”
                    }
                }
    }
}
}
