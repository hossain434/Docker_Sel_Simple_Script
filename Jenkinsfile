pipeline {
  agent {
    node {
      label 'maven'
    }

  }
  stages {
    stage('Build Jar') {
      steps {
       bash sh 'mvn clean package -DskipTests'
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
