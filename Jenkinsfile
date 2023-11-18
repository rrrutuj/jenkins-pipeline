pipeline {
    agent none
    stages {
        stage('Run Tests') {
            agent {
                docker { image 'node:16-alpine' }
            }
            steps {
                script {
                        sh 'ls'
                        // Run your React tests (replace 'test' with your actual test script/command)
                        dir('${WORKSPACE}/react-java-mysql/frontend') {
                            sh 'npm test'
                            sh 'cd ..'
                        }
                }
            }
        }
        stage('Build and Test') {
            agent {
                docker { image 'maven:3.8.1-adoptopenjdk-11' }
            }
            steps {
                script {
                    dir('${WORKSPACE}/react-java-mysql/backend') {
                        sh 'mvn clean test'
                    }
                }
            }
        }
        stage('deploy') {
            agent any
            steps {
                sh 'docker compose -f ${WORKSPACE}/react-java-mysql/compose.yaml up -d'
            }
        }
    }
}