pipeline { agent any

stages {
    stage('Checkout') {
        steps {
            git 'https://github.com/your-repo.git'
        }
    }
    
    stage('Build') {
        steps {
            sh 'docker build -t your-image .'
        }
    }
    
    stage('Test') {
        steps {
            sh 'docker run your-image npm test'
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
