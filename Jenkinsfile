pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        DOCKER_HUB_USER = "kiruthikakeeka"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/kiruthikakeeka/cicd-jenkins-docker.git'
            }
        }

        stage('Code Quality Check') {
            steps {
                echo 'Running SonarQube Analysis...'
                sh 'sonar-scanner -Dsonar.projectKey=myapp'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'docker-hub-password', variable: 'DOCKER_PASS')]) {
                    sh "docker login -u ${DOCKER_HUB_USER} -p ${DOCKER_PASS}"
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                sh 'docker-compose -f docker-compose.yml up -d'
                echo 'Deployed to Staging successfully!'
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve Production Deployment?', ok: 'Deploy'
                sh 'docker-compose -f docker-compose.yml up -d'
                echo 'Deployed to Production successfully!'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}
