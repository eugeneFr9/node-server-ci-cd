pipeline {
   agent any

   environment {
     // You must set the following environment variables
     // ORGANIZATION_NAME
     // YOUR_DOCKERHUB_USERNAME (it doesn't matter if you don't have one)

     SERVICE_NAME = "node-server"
     REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${SERVICE_NAME}:${BUILD_ID}"
   }

   stages {
        stage('Cloning our Git') { 
            steps { 

                git 'https://github.com/genegr88/node-server-ci-cd' 
            }
        } 
      stage('Build') {
         steps {
            'echo hello'
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'docker image build -t ${REPOSITORY_TAG} .'
         }
      }

      stage('Deploy to Cluster') {
          steps {
                    sh 'envsubst < ${WORKSPACE}/deployment.yaml | kubectl apply -f -'
          }
      }
   }
}