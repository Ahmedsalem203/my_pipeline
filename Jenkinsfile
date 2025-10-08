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
               docker biuld -t $IMAGE_NAME:$TAG .
          '''
      }
    }
    stage('test'){
      steps{
        sh '''
            echo "testing stage"
          '''
      }
    }
    stage('deploy'){
      steps{
        sh '''
            echo "deploying stage"
          '''
      }
    }
  }
}
