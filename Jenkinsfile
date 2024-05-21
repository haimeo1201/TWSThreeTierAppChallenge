pipeline {
    agent any

    stages {
        stage('SCM') {
            checkout scm
        }
        stage('SonarQube Analysis') {
            def scannerHome = tool 'sonarqube';
            withSonarQubeEnv() {
                sh "${scannerHome}/bin/sonar-scanner"
            }
        }

        stage('Build and Push Frontend Docker Image') {
            steps {
                script {
                        sh "docker login --username haimeo1201 --password dctun1234"
                        sh "docker build -t fe frontend"
                        sh "docker tag fe haimeo1201/fecicd:v1.1"
                        sh "docker push haimeo1201/fecicd"
                }
            }
        }

        stage('Build and Push Backend Docker Image') {
            steps {
                script {
                    // Build and push the backend Docker image to ECR
                    sh "docker build -t be backend"
                    sh "docker tag be haimeo1201/becicd:v1.1"
                    sh "docker push haimeo1201/becicd"
                }
            }
        }
      }
    }
