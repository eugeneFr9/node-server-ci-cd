pipeline {
   agent any

   environment {

     SERVICE_NAME = 'node-server'
     REPOSITORY_TAG="${DOCKERHUB}/${SERVICE_NAME}:${BUILD_ID}"
     registryCredential = 'dockerhub'
     dockerImage = ''
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git 'git@github.com:genegr88/node-server-ci-cd.git'
         }
      }
   stage('Build') {
         steps {
            echo 'Buidling.....'
         }
      }

   stage('Building image') {
      steps{
        script {
          dockerImage = docker.build ${REPOSITORY_TAG}
        }
      }
    }

    stage('Deploy Image') {
      steps{    
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
      }
    }
  }
    }

      stage('Deploy to Cluster') {
          steps {
                    sh 'envsubst < ${WORKSPACE}/deployment.yaml | kubectl apply -f -'
          }
      }
   }
}