pipeline {
  agent any

  environment {
    DOCKER_IMAGE_BACKEND = "student-absence-app-backend"
    DOCKER_IMAGE_FRONTEND = "student-absence-app-frontend"
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/hiba123887/student-absence-app.git'
        sh 'ls -l'
      }
    }

    stage('Install Backend Dependencies') {
      agent {
        docker {
          image 'node:18-alpine'
          args "-v $WORKSPACE:$WORKSPACE -w $WORKSPACE"
        }
      }
      steps {
        dir('backend') {
          sh 'npm install'
        }
      }
    }

    stage('Install Frontend Dependencies') {
      agent {
        docker {
          image 'node:18-alpine'
          args "-v $WORKSPACE:$WORKSPACE -w $WORKSPACE"
        }
      }
      steps {
        dir('frontend') {
          sh 'npm install'
        }
      }
    }

    stage('Run Backend Tests') {
      agent {
        docker {
          image 'node:18-alpine'
          args "-v $WORKSPACE:$WORKSPACE -w $WORKSPACE"
        }
      }
      steps {
        dir('backend') {
          sh 'npm test'
        }
      }
    }

    stage('Run Frontend Tests') {
      agent {
        docker {
          image 'node:18-alpine'
          args "-v $WORKSPACE:$WORKSPACE -w $WORKSPACE"
        }
      }
      steps {
        dir('frontend') {
          sh 'npm test'
        }
      }
    }

    stage('Docker Compose') {
      steps {
        sh 'docker-compose build'
      }
    }

    stage('Push Images') {
      steps {
        echo "Push vers registry si configuré"
        // Exemple :
        // sh "docker-compose push"
      }
    }

    stage('Deploy with Ansible') {
      steps {
        sh 'ansible-playbook ansible/playbook.yml'
      }
    }
  }
}
