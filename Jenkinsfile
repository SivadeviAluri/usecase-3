pipeline {
    agent any

    stages {
        stage('Clone Repository'){
            steps{
                checkout scm
            }
        }
    }
    stage('Build Docker images in parallel') {
        parallel{
            stage('Build python image'){
                steps{
                    dir('python')
                    sh 'docker build -t devi819/python_image:latest .'
                }
            }
            stage('Build java image'){
                steps{
                    dir('java'){
                        sh 'docker build -t devi819/java_image:latest .'
                    }
                }
            }
            stage('Build nginx image'){
                steps{
                    dir('nginx'){
                        sh 'docker build -t devi819/nginx_image:latest .'
                    }
                }
            }
        }
    }
    stage('Push to Dockerhub') {
        steps{
            sh """
            docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
            docker push devi819/python_image:latest
            docker push devi819/java_image:latest
            docker push devi819/nginx_image:latest
            """
        }
        environment{
           DOCKERHUB_CREDENTIALS = credentials('hello') 
        }
    }
}
