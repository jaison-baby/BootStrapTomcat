pipeline {
    agent any
	
     
//  stage('Publish image to Docker Hub') {
//          
//            steps {
//        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
//          sh  'docker push nikhilnidhi/samplewebapp:latest'
//        //  sh  'docker push nikhilnidhi/samplewebapp:$BUILD_NUMBER' 
//        }
//                  
//          }
//        }
     
//      stage('Run Docker container on Jenkins Agent') {
//             
//            steps 
//			{
//                sh "docker run -d -p 8003:8080 nikhilnidhi/samplewebapp"
// 
//            }
//        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                 script {
                    withCredentials([sshUserPrivateKey(credentialsId: 'Jenkins-user', keyFileVariable: 'SSH_KEY')]) {
                    sh 'scp -i \${SSH_KEY} -v -o StrictHostKeyChecking=no -r /home/ubuntu/tomcat/CI-CD-using-Docker/target/LoginWebApp-1.war  ubuntu@34.121.68.53: /home/ubuntu/tomcat/CI-CD-using-Docker/target/LoginWebApp-1.war' }
sh “docker-compose up -d ”
                    }
 
            }
        }
    }
	}
    
