pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "manjunathbm2003/devops-app"
        DOCKER_USER  = "manjunathbm2003"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'TOKEN')]) {
                    sh 'echo $TOKEN | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE'
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh 'ansible-playbook playbook.yml'
            }
        }
    }
}
