pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                checkout scm
            }
        }
        stage("Test") {
            steps {
                sh 'npm install'
                sh 'npm test'
            }
        }
        stage("Build") { 
            steps {
                sh 'npm run build'  
            }
        }
        stage("Build Image") { 
            steps {
                sh 'docker build -t node-app-test:1.0 .'  
            }
        }
        stage("Push image") {
            steps {
               withCredentials([usernamePassword(credentialsID: 'dockerhub', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) { 
                   sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                   sh 'docker tag node-app-test:1.0 deepikaambu/node-app-test:1.0'
                   sh 'docker push deepikaambu/node-app-test:1.0'
                   sh 'docker logout'
               }
            }    
        }
  }
}
    
    
