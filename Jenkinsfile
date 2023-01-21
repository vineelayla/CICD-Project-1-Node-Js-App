pipeline{
    agent any
    
    environment{
        registry = "jaydeep007docker"
        registryCredential = 'c468ea58-6880-4e27-8190-5efb7f1dd07f'        
               }
    
    stages{
       stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
       stage('Deploy Image') {
      steps{
         steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                    sh 'docker push myimage:latest'
                }
        }
      }
    }
  }
}