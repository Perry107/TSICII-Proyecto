pipeline {
  environment {
    dockerimagename = "perry107/phpmyadmin:phpmyadmincard"
    dockerImage = "perry107/phpmyadmin:phpmyadmincard"
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Perry107/TSICII-Proyecto']]])
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }
    stage('Pushing Image') {
      environment {
               registryCredential = 'docker'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("v1")
          }
        }
      }
    }
    stage('Deploying card to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: 'phpmyadmin-deployment.yaml',kubeconfigId: 'k8s')
        }
      }
    }
  }
}
