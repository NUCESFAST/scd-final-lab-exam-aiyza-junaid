pipeline {
    agent any

    stages {
        stage('i211145_Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/NUCESFAST/scd-final-lab-exam-aiyza-junaid.git'
            }
        }

        stage('i211145_Dependency Installation') {
            steps {
                bat 'npm install' 
            }
        }

        stage('i211145_Build and Push Auth Backend Image') {
            steps {
                script {
                    docker.build('aiyzajunaid/auth-backend:latest', './Auth')
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('aiyzajunaid/auth-backend:latest').push()
                    }
                }
            }
        }

        stage('i211145_Build and Push Classroom Service Image') {
            steps {
                script {
                    docker.build('aiyzajunaid/classroom-service:latest', './Classrooms')
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('aiyzajunaid/classroom-service:latest').push()
                    }
                }
            }
        }

        stage('i211145_Build and Push Post Service Image') {
            steps {
                script {
                    docker.build('aiyzajunaid/post-service:latest', './Post')
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('aiyzajunaid/post-service:latest').push()
                    }
                }
            }
        }

        stage('i211145_Build and Push Event Bus Service Image') {
            steps {
                script {
                    docker.build('aiyzajunaid/eventbus-service:latest', './event-bus')
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('aiyzajunaid/eventbus-service:latest').push()
                    }
                }
            }
        }

        stage('i211145_Build and Push React Frontend Image') {
            steps {
                script {
                    docker.build('aiyzajunaid/react-frontend:latest', './client')
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credentials') {
                        docker.image('aiyzajunaid/react-frontend:latest').push()
                    }
                }
            }
        }

        stage('i211145_Run Docker Compose') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
