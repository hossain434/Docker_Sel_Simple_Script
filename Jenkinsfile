pipeline {
    agent {
        node {
            label 'docker' && 'maven'
        }
            tools { 
        maven 'Maven 3.3.9' 
        jdk 'jdk8' 
    }
    }
    stages {    
        stage('Build Jar') {
            steps {
                bat 'mvn clean install package'
            }
        }
        stage('Build Image') {
            steps {
                script {
                      // vinsdocker/containertest => organization/application - it could be anything
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
