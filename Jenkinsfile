pipeline {
    agent any
    tools {
        nodejs "nodejs"
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
                sh 'docker build -t 20127050/onlineacademy:latest .'
                sh 'docker tag onlineacademy 20127050/onlineacademy:latest'
            }
        }
        stage('Docker push') {
            steps {
                withDockerRegistry([credentialsId: "dockerHub", url: ""]) {
                    sh 'docker push 20127050/onlineacademy:latest'
                }
            }
        }
        stage('Docker deploy') {
            steps {
                sh 'ssh -i /home/keys/192.168.64.130/id_rsa -o StrictHostKeyChecking=no user-20127540@192.168.64.130 docker run -d -p 8003:5000 20127050/onlineacademy'
            }
        }
    }
}