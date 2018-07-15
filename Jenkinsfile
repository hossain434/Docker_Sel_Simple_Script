pipeline {
    agent {
        node {
            label 'docker' && 'maven'
        }
    }
    stages {    
        stage('Build Jar') {
            steps {
                bat "mvn clean install"
            }
        }
        stage('Build Image') {
            steps {
                script {
                      // vinsdocker/containertest => organization/application - it could be anything
                      app = docker.build("vinsdocker/containertest")
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
