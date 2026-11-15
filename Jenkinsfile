
pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Fetching source code from GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Java application'
                bat 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Java application'
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Creating JAR file'
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application'

                bat '''
                if not exist "D:\\P3\\deployment" mkdir "D:\\P3\\deployment"
                copy /Y target\\jenkins-maven-demo-1.0.jar D:\\P3\\deployment\\
                '''

                archiveArtifacts artifacts: 'target/*.jar',
                                 fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}
