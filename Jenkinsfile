pipeline {
   agent any
   stages {
      stage('Checkout Code') {
         steps {
              checkout scm
         }
      }
      stage('Install Dependencies') {
         steps {
             sh 'npm install'
         }
      }
      stage('Build Application') {
         steps {
             sh 'npm run build'
         }
      }
      stage('Docker Build') {
         steps {
             sh 'docker build -t todo-app .'
         }
      }
      stage('Dockerhub Repository') {
         steps {
            sh 'docker push luqzi/todo-app:latest'
         }
      }
      stage('Deploy to VM2') {
         steps {
             sh '''
               ssh -o StrictHostKeyChecking=no ubuntu@65.0.124.23
               docker stop todo-app || true
               docker rm todo-app || true
               docker pull luqzi/todo-app:latest
               docker run -d --name todo-app -p 3000:3000 luqzi/todo-app:latest
            '''
         }
      }
   }
}
