pipeline {
    environment{
        imageName=""
    }
    agent any
    stages {
        stage('Github clone react') {
            steps {
                git branch:'main', url : 'https://github.com/anshulsankhyan/student-sphere-frontend.git'
            }
        }
        stage('Build React') {
            steps {
                script{
                    sh 'npm install'
                }
            }
        }
        stage('Github clone spring') {
            steps {
                git branch:'main', url : 'https://github.com/anshulsankhyan/student-sphere-backend.git'
            }
        }
        stage('Maven Build Spring') {
            steps {
                script{
                    sh 'mvn clean install'
                }
            }
        }
        stage('Github clone for docker build react') {
            steps {
                git branch:'main', url : 'https://github.com/anshulsankhyan/student-sphere-frontend.git'
            }
        }
        
        stage('Docker Build React') {
            steps {
                script{
                    imageName=docker.build "anshulsankhyan98/spe_major_project_frontend"
                }
            }
        }
        stage('Push Docker Image React') {
            steps {
                script{
                    docker.withRegistry('','docker-jenkins'){
                        imageName.push()
                    }
                }
            }
        }
        stage('Github clone for docker build spring') {
            steps {
                git branch:'main', url : 'https://github.com/anshulsankhyan/student-sphere-backend.git'
            }
        }
        stage('Docker Build Spring') {
            steps {
                script{
                    imageName=docker.build "anshulsankhyan98/spe_major_project_backend"
                }
            }
        }
        stage('Push Docker Image Spring') {
            steps {
                script{
                    docker.withRegistry('','docker-jenkins'){
                        imageName.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook credentialsId: 'check',colorized: true, installation: 'Ansible', inventory: 'inventory',
                 playbook: 'playbook.yml'
            }
        }
    }
}
