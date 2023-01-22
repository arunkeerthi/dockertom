pipeline {
    agent any
	
	  tools
    {
       maven "Maven"
    }
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/arunkeerthi/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp arunkeerthi3101/samplewebapp:latest'
                //sh 'docker tag samplewebapp arunkeerthi3101/samplewebapp:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "Docker_hub", url: "" ]) {
          sh  'docker push arunkeerthi3101/samplewebapp:latest'
        //  sh  'docker push arunkeerthi3101/samplewebapp:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8005:8080 arunkeerthi3101/samplewebapp"
 
            }
        }
    }
	}
    
