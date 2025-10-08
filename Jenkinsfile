pipeline{
  agent any
  environment{
       IMAGE_NAME = "myapp"       
       TAG = "latest"   
  }
  stages{
    stage('Build Docker Image'){
      steps{
        sh '''
               echo "Building Docker image..."
               docker build -t $IMAGE_NAME:$TAG .
          '''
      }
    }
     stage('Push Image to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'my_docker_hup', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh """
                        echo "Logging in to Docker Hub..."
                        docker login -u $DOCKER_USER -p $DOCKER_PASS
                 

                        echo "Tagging image..."
                        docker tag $IMAGE_NAME:$TAG $DOCKER_USER/$IMAGE_NAME:$TAG

                        echo "Pushing image to Docker Hub..."
                        docker push $DOCKER_USER/$IMAGE_NAME:$TAG

                        echo "Logging out..."
                        docker logout
                    """
                }
            }
        }
    stage('Deploy Container') {
            steps {
                script {
                    sh """
                        echo "Deploying container..."
                        docker rm -f ${IMAGE_NAME}_container || true
                        docker run -d -p 8081:80 --name ${IMAGE_NAME}_container $IMAGE_NAME:$TAG
                        echo "✅ Container is running on http://localhost:8080"
                    """
                }
            }
        }

  }
}
