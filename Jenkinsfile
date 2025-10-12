pipeline{
  agent any
  environment{
       IMAGE_NAME = "myapp"       
       TAG = "latest"   
  }
  stages{
     stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: '*/main']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [[$class: 'CloneOption', noTags: false, shallow: false, depth: 0]],
                    userRemoteConfigs: [[url: 'https://github.com/Ahmedsalem203/my_pipeline.git']]
                ])
            }
        }
     stage ("build docker")
      {
          steps 
          {
              sh """
                  docker build -t docker.io/ahmed1salem/my-docker:v1 .
              """
          }
      }

      stage ("push image")
      {
          steps 
          {
              withCredentials([usernamePassword(credentialsId: 'my_docker_hup', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) 
              {
                  sh """
                      docker login -u \$DOCKER_USER -p \$DOCKER_PASS
                      docker push docker.io/ahmed1salem/my-docker:v1
                  """
              }
          }
      }

  }
}
