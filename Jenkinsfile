pipeline {
    agent any
	
	
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/BhavanDevOps/CI-CD-using-Docker.git'
             
          }
        }

  stage('Docker Build and Tag') {
           steps {
              
                sh 'sudo docker build -t samplewebapp:latest .' 
                sh 'sudo docker tag samplewebapp nikhilnidhi/samplewebapp:latest'
                //sh 'sudo docker tag samplewebapp nikhilnidhi/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
          sh  'sudo docker push bhavan1210/samplewebapp:latest'
        //  sh  'sudo docker push bhavan1210/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "sudo docker run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
            }
        }
 stage('Run Docker container on remote hosts') {
             
            steps {
                sh "sudo docker -H ssh://jenkins@54.82.49.205 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
            }
        }
    }
	}
    
