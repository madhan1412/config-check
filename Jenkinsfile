pipeline {
  agent any
  stages {
      stage('Build Image') {
          steps {
             echo 'Starting to build docker Image'
    
             script {
                 def dockerfile = 'Dockerfile'
                 def customImage = docker.build('rbi-docker/sessionmanager:latest', "-f ${dockerfile} .")
                     }
                 }
           }
      stage('Test') {
          steps {
              echo 'Test..'
          }
      }
      stage('server') {
         steps {
             rtServer (
                 //id: 'Artifactory-1',
                 url: 'https://us-artifactory.cicd.cloud.fpdev.io/ui/admin/artifactory',
                 //credentialsId: 'my-credentials-id'
                 X-JFrog-Art-Api: 'AKCp8k8PiJAEWjtfRWLcRQFqurF6BqArTp1zTTUYFsddoLMmVzj53njcVsaM5MLnSQ1AJotfL'
                      ) 
            
               }
       }
       stage('upload to Artifactory'){
          steps{
              rtDockerPush(
                  //serverId: 'Artifactory-1',
                  X-JFrog-Art-Api: 'AKCp8k8PiJAEWjtfRWLcRQFqurF6BqArTp1zTTUYFsddoLMmVzj53njcVsaM5MLnSQ1AJotfL',
                  image: 'rbi-docker/sessionmanager:latest',
                  //host: HOST_NAME,
                  targetRepo: 'rbi-docker',
                  
                  //properties: 'project-name=docker1;status=stable',  samp;
                  //project: 'my-project-key',
                  
                          )
               
               
              }
           }
      }
  }
