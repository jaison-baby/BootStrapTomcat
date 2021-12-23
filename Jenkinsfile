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
                      image 'maven:3.6.3'
                      args '--user 0:0'
                  }
          }
          steps {
                
                sh "mvn clean install"
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'b2fba6f9-e9e7-4198-9ac7-8c3d8a4a4645', keyFileVariable: 'SSH_KEY')]) {
                    sh 'scp -i \${SSH_KEY} -v -o StrictHostKeyChecking=no -r /var/lib/jenkins/workspace/NewDocker_main@2/target/LoginWebApp-1.war ubuntu@3.21.210.44:/home/ubuntu/latest/BootStrapTomcat/target/' }
sh “docker-compose up -d”
                    }
                }
    }
}
}
