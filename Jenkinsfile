pipeline{
  agent any

  stages{
     
  //    stage ("build docker")
  //     {
  //         steps 
  //         {
  //             sh """
  //                 docker build -t docker.io/ahmed1salem/my-docker:v1 .
  //             """
  //         }
  //     }

  //     stage ("push image")
  //     {
  //         steps 
  //         {
  //             withCredentials([usernamePassword(credentialsId: 'my_docker_hup', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) 
  //             {
  //                 sh """
  //                     docker login -u \$DOCKER_USER -p \$DOCKER_PASS
  //                     docker push docker.io/ahmed1salem/my-docker:v1
  //                 """
  //             }
  //         }
  //     }
    stage ("Deploy")
    {
        steps 
        {
            sshagent(credentials: ['ssh-key']) 
            {
                sh """
                    ssh -o StrictHostKeyChecking=no ubuntu@34.228.241.65 '
                    touch file-from-Jenkins
                    '
                """
            }
        }
    }

  }
}
