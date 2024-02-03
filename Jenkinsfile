pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                sh 'echo passed'
                //git branch: 'main', url: 'https://github.com/fatimatabassum1/Jenkins-Zero-To-Hero'
            }
        }
        stage('Build and Test') {
            steps {
                // build the project and create a JAR file
                sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app && mvn clean package'
            }
        }
        stage('Build and Push Docker Image') {
            environment {
                DOCKER_IMAGE = "fatimatassum/ultimate-cicd-new:${BUILD_NUMBER}"
                // DOCKERFILE_LOCATION = "java-maven-sonar-argocd-helm-k8s/spring-boot-app/Dockerfile"
                REGISTRY_CREDENTIALS = credentials('docker-cred')
                }
            steps {
                script {
                    sh 'cd java-maven-sonar-argocd-helm-k8s/spring-boot-app && docker build -t ${DOCKER_IMAGE} .'
                    def dockerImage = docker.image("${DOCKER_IMAGE}")
                    docker.withRegistry('https://index.docker.io/v1/', "docker-cred") {
                    dockerImage.push()
                    }
                }
            }
        }
    }
}
