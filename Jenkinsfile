pipeline {
  agent any 

  stages {
    stage('i211145_Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/NUCESFAST/scd-final-lab-exam-aiyza-junaid'
      }
    }

    stage('i211145_Dependency Installation') {
      steps {
        // Install dependencies for Auth backend
        bat 'cd Auth && npm install'
        // Install dependencies for Classroom service
        bat 'cd Classrooms && npm install'
        // Install dependencies for Post service
        bat 'cd Post && npm install'
        // Install dependencies for Event Bus service
        bat 'cd event-bus && npm install'
        // Install dependencies for React frontend
        bat 'cd client && npm install'
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