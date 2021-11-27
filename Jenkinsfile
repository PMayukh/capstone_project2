pipeline {

agent any

    tools{
        maven 'mymaven'
        jdk 'myjava'
    }

stages {

stage('Checkout the code'){
           steps{
             git url: 'https://github.com/PMayukh/capstone_project2.git', branch: 'master'
           }
}

      stage('Build test and Package '){
      
           steps{
               sh """
               mvn package
               """
           }
       }

stage('Build and Push Image'){
steps {
 script{
   docker.withRegistry('https://registry.hub.docker.com', 'docker_hub') {

        def customImage = docker.build("pmayukh/capjavaapp:${env.BUILD_NUMBER}")

        /* Push the container to the custom Registry */
        customImage.push()
    }
    }
   }
  }   

    stage('Run the docker image'){
     steps{
      
         sh """
         docker run -it -d -p 8123:8123 pmayukh/capjavaapp:${env.BUILD_NUMBER}
         """
         }
   }        
    
   
 }

post {

          always{
              echo "Job Completed"
          }
      }   

}
