pipeline {
  agent {
    node {
      label 'maven'
    }

  }
 
    stage('Build Image') {
      steps {
        script {
          app = docker.build("arif/test")
        }

      }
    }
    stage('Push Image') {
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${BUILD_NUMBER}")
            app.push("latest")
          }
        }

      }
    }
  }
}
