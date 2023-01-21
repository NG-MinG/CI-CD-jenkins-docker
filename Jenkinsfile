pipeline {
    agent any
    tools {
        nodejs "nodejs"
    }
    environment {
        dockerhub = credentials('c3244f57-9392-4987-a76f-00b9533c5c0a')
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/20127050/CI-CD-jenkins-docker.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Docker build') {
            steps {
                sh 'docker build -t onlineacademy:latest .'
            }
        }
        stage('Docker push') {
            steps {
                sh 'docker tag onlineacademy:latest 20127050/onlineacademy:latest'
                sh 'echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin'
                
                sh 'docker push 20127050/onlineacademy:latest'
            }
        }
        stage('Docker deploy') {
            steps {
                sh 'ssh -i /home/keys/192.168.64.130/id_rsa -o StrictHostKeyChecking=no user-20127540@192.168.64.130 docker run -d -p 8003:5000 20127050/onlineacademy'
            }
        }
    }
}