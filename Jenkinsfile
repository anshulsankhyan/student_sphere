pipeline {
    environment {
        imageName = ""
    }
    agent any
    stages {
        stage('Github clone react') {
            steps {
                git branch: 'main', url: 'https://github.com/anshulsankhyan/student-sphere-frontend.git'
            }
        }
        stage('Build React') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }
        stage('Github clone spring') {
            steps {
                git branch: 'main', url: 'https://github.com/anshulsankhyan/student-sphere-backend.git'
            }
        }
        stage('Maven Build Spring') {
            steps {
                script {
                    sh 'mvn clean install'
                }
            }
        }
        stage('Clone React Docker File') {
            steps {
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/anshulsankhyan/student-sphere-frontend.git'
            }
        }
        stage('Build and push React Docker image') {
            steps {
                script {
                    docker.buildAndPush(
                        context: '.',
                        dockerfile: 'path/to/student-sphere-frontend/Dockerfile',
                        imageName: 'anshulsankhyan98/spe_major_project_frontend:latest'
                    )
                }
            }
        }
        stage('Clone SpringBoot Dockerfile') {
            steps {
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/anshulsankhyan/student-sphere-backend.git'
            }
        }
        stage('Build and push SpringBootDocker image') {
            steps {
                script {
                    docker.buildAndPush(
                        context: '.',
                        dockerfile: 'path/to/student-sphere-backend/Dockerfile',
                        imageName: 'anshulsankhyan98/spe_major_project_backend'
                    )
                }
            }
        }
        stage('Deploy') {
            steps {
                ansiblePlaybook becomeUser: null, colorized: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: 'inventory',
                 playbook: 'playbook.yml', sudoUser: null
            }
        }
    }
}
