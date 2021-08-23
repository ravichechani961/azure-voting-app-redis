pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            sh('docker images -a')
            sh("""
               cd azure-vote/
               docker images -a
               docker build -t jenkins-pipeline .
               docker images -a
               cd ..
            """)
         }
      }
      stage('Push container') {
         steps {
            echo "workspace is $WORKSPACE"
            dir ("$WORKSPACE/azure-vote"){
               script{
                  docker.withRegistry('https://index.docker.io/v1/','DockerHub'){
                     def image= docker.build('blackdentech/jenkins-course:latest')
                     image.push()
                  }
               }
            }
          
         }
      }
      
     
      
   }
}
