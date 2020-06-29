pipeline {
   agent any
   environment {
       registry = "samridhi9719/jenkins_mvn"
       registryCredential= 'dockerhub'
       dockerImage=''
   }

   stages {
      stage('SCM checkout') {
         steps {
            git 'https://github.com/samridhi97/docker_maven.git'
         }
      }
      stage('Build Docker Image') {
         steps {
            script{
               dockerImage= docker.build registry + ":$BUILD_NUMBER"
            }
         }
      }
      stage('Deploy Image') {
         steps {
            script{
               docker.withRegistry('https://registry.hub.docker.com',registryCredential ){
                   dockerImage.push()
               }
            }
         }
      }
      stage('Remove Image') {
         steps {
            sh "docker rmi $registry:$BUILD_NUMBER"
         }
      }
   }
}
