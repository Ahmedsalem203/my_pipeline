pipeline{
  agent any
  tools{
    nodejs 'node 24.9.0'
  }
  stages{
    stage('Check NPM version'){
      steps{
        sh '''
             npm -v
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
