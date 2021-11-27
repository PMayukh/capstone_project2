pipeline {

agent any

    tools{
        maven 'mymaven'
        jdk 'myjava'
    }

stages {

stage('Checkout the code'){
           steps{
             git url: 'https://github.com/PMayukh/PG_Devops_Project.git', branch: 'master'
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

        def customImage = docker.build("pmayukh/javaapp:${env.BUILD_NUMBER}")

        /* Push the container to the custom Registry */
        customImage.push()
    }
    }
   }
  }   

 }

post {

          always{
              echo "Job Completed"
          }
      }   

}
