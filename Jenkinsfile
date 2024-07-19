pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'kiranss499@gmail.com', url: 'https://github.com/kirankiler9908/Angular-HelloWorld/'
                  sh 'ls -la'
            }
        }
       
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("killer9908/ch:${env.BUILD_ID}", "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'dockerhub') {
                        docker.image("killer9908/ch:${env.BUILD_ID}").push()
                    }
                }
            }
        }
    }

  post {
     always {
          cleanWs()
       }
 }
}
