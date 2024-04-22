pipeline {
    agent any 
    
    stages { 
        stage('Checkout') {
            steps {
                git 'https://github.com/wasAmesha/4257-Wahalathanthri'
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t ameshawas/adder-app:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerPassword', variable: 'dockerPassword')]) {
                    script {
                        bat "docker login -u ameshawas -p ${dockerPassword}"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push ameshawas/adder-app:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}

