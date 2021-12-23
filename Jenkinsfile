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
                sh “source /etc/profile.d/maven.sh”
                sh "mvn clean install"
                script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'ubuntu', keyFileVariable: 'SSH_KEY')]) {
                    sh 'scp -i \${SSH_KEY} -v -o StrictHostKeyChecking=no -r /home/ubuntu/nexus-backend/target/spring-boilerplate-1.0.0.war ubuntu@34.121.68.53: /home/ubuntu/livespace-dev/livespace-app/' }
sh “docker-compose up -d && docker-compose restart livespace-app”
                    }
                }
    }
}
}
