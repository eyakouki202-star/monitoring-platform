pipeline {
  agent any
  environment {
   DOCKER_USER = "eyakouki"
  }
  stages {
    stage("Build") {
    steps {
         sh "docker build -t $DOCKER_USER/monitoring-tshark:latest docker/tshark"
     sh "docker build -t $DOCKER_USER/monitoring-smokeping:latest docker/smokeping"
      sh "docker build -t $DOCKER_USER/monitoring-ntopng:latest docker/ntopng"
      }
   }
    stage("Push") {
      steps {
        withCredentials([usernamePassword(credentialsId: "dockerhub-creds", usernameVariable: "U", passwordVariable: "P")]) {
          sh "echo \$P | docker login -u \$U --password-stdin"
         sh "docker push $DOCKER_USER/monitoring-tshark:latest"
         sh "docker push $DOCKER_USER/monitoring-smokeping:latest"
         sh "docker push $DOCKER_USER/monitoring-ntopng:latest"
        }
      }
    }
    stage("Deploy") {
      steps {
         sh "kubectl apply -f k8s"
      }
    }
    }
  }
}
