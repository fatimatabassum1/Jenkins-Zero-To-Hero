pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                git credentialsId: 'gph_qCFUwO1tWMjx1794ObXz5iQLkibeYL0g1HsS',
                url: 'https://github.com/fatimatabssum1/Jenkins-Zero-To-Hero',
                branch: 'main'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t fatimatabassum/cicd-new:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push fatimatabssum/cicd-new:${BUILD_NUMBER}
                    '''
                }
            }
        }
    }
}
