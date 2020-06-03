pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    sh './gradlew clean build -x test --no-daemon'
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    sh './gradlew test --no-daemon'
                }
            }
        }
        stage('Static code analysis') {
            steps {
                script {
                    sh './gradlew checkstyleMain --no-daemon' //run a gradle task
                }
            }
        }
        stage('Deploy') {
            environment {
                HEROKU_API_KEY = credentials('heroku-api-key-joran')
            }
            steps {
                script {
                    sh './gradlew deployHeroku --no-daemon' //run a gradle task
                }
            }
        }
    }
}