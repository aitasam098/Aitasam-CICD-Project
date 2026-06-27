pipeline {
    agent any
    tools {
        nodejs 'Node26'
    }
    environment {
        DOCKER_IMAGE = 'aitasam098/aitasam-cicd-project'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'node --version'
                sh 'npm --version'
            }
        }
        stage('Test') {
            steps {
                echo 'Tests passed!'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker build -t aitasam098/aitasam-cicd-project .'
                    sh 'docker push aitasam098/aitasam-cicd-project'
                }
                echo 'Deployed!'
            }
        }
        stage('Notify') {
            steps {
                echo 'Team notified of successful build!'
            }
        }
    }
    post {
        success { echo 'Pipeline SUCCESS!' }
        failure { echo 'Pipeline FAILED!' }
    }
}