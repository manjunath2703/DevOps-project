pipeline {
agent any

stages {

stage('Clone Repository') {
steps {
git branch: 'main', url: 'https://github.com/manjunath2703/DevOps-project.git'
}
}

stage('Build Docker Image') {
steps {
sh 'docker build -t Devops-app .'
}
}

stage('Docker Login') {
steps {
withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
sh 'echo $PASS | docker login -u $USER --password-stdin'
}
}
}

stage('Push Docker Image') {
steps {
sh 'docker tag Devops-app manjunathbm2003/Devops-app:latest'
sh 'docker push manjunathbm2003/Devops-app:latest'
}
}

stage('Deploy using Ansible') {
steps {
sh 'ansible-playbook -i inventory playbook.yml'
}
}

}
}
