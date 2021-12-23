pipeline {
    agent any
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
                    sh 'scp -i \${SSH_KEY} -v -o StrictHostKeyChecking=no -r /home/ubuntu/latesr/BootStrapTomcat/target/LoginWebApp-1.war ubuntu@:3.21.210.44 /home/ubuntu/latesr/BootStrapTomcat/target/LoginWebApp-1.war' }
sh “docker-compose up -d”
                    }
                }
     }
}
}
