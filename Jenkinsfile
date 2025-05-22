pipeline {
  agent any

  environment {
    DOCKER_IMAGE_BACKEND = "student-absence-backend"
    DOCKER_IMAGE_FRONTEND = "student-absence-frontend"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/hiba123887/student-absence-app.git'
      }
    }

      steps {
        dir('backend') {
          sh 'npm install'
        }
      }
    }

  
      steps {
        dir('backend') {
          sh 'npm test'
        }
      }
    }

    stage('Build Backend Docker Image') {
      steps {
        dir('backend') {
          sh "docker build -t ${DOCKER_IMAGE_BACKEND} ."
        }
      }
    }

    stage('Build Frontend Docker Image') {
      steps {
        dir('frontend') {
          sh "docker build -t ${DOCKER_IMAGE_FRONTEND} ."
        }
      }
    }

    stage('Push Images') {
      steps {
        echo "Push vers registry si configuré"
      }
    }

    stage('Deploy with Ansible') {
      steps {
        sh 'ansible-playbook ansible/playbook.yml'
      }
    }
  }
}
