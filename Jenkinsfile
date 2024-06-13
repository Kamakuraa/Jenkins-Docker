pipeline 
{ 
    agent any

stages {
    stage('Checkout main branch') {
        steps {
           checkout scm  
        }
    }
    
    stage('Build') {
        steps {
            sh 'docker build -t your-image .'
        }
    }
    
    stage('Test') {
        steps {
            sh 'docker run --name test-container -p 3000:3000 -d your-image'
        }
    }
    
    stage('Push to DockerHub') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                sh "docker tag your-image your-dockerhub-username/your-image"
                sh "docker push your-dockerhub-username/your-image"
              }
          }
      }
   }
}
