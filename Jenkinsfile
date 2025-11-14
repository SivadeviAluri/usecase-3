pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS = credentials('hello')
    }
    
    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Images in Parallel') {
            parallel {
                stage('Build Python Image') {
                    steps {
                        dir('python') {
                            sh 'docker build -t devi819/python_image:latest .'
                        }
                    }
                }
                
                stage('Build Java Image') {
                    steps {
                        dir('java') {
                            sh 'docker build -t devi819/java_image:latest .'
                        }
                    }
                }
                
                stage('Build Nginx Image') {
                    steps {
                        dir('nginx') {
                            sh 'docker build -t devi819/nginx_image:latest .'
                        }
                    }
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                sh """
                    docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                    docker push devi819/python_image:latest
                    docker push devi819/java_image:latest
                    docker push devi819/nginx_image:latest
                """
            }
        }
    }
}
