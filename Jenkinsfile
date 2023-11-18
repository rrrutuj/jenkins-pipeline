pipeline {
    agent any
    environment {
        // Customize these variables based on your project structure
        NODEJS_HOME = '/usr/local/bin/node'
        NPM_HOME = '/usr/local/bin/npm'
    }
    stages {
        stage('Fetch repository') {
            steps {
                git 'https://github.com/prasad1825/awesome-compose.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    // Install Node.js and npm
                    env.PATH = "${NODEJS_HOME}:${NPM_HOME}:${env.PATH}"
                    sh 'npm install'
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                        // Run your React tests (replace 'test' with your actual test script/command)
                        dir('${WORKSPACE}/react-java-mysql/frontend') {
                            sh 'npm test'
                            sh 'cd ..'
                        }
                }
            }
        }
        stage('Build and Test') {
            steps {
                script {
                    // Set the environment variables
                    env.PATH = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${env.PATH}"
                    MAVEN_OPTS = "-Dmaven.repo.local=${WORKSPACE}/.m2/repository -Duser.home=${WORKSPACE}"

                    // Run Maven tests
                    sh "mvn clean test -s ${MAVEN_SETTINGS}"
                }
            }
        }
        stage('deploy') {
            steps {
                sh 'docker compose -f ${WORKSPACE}/react-java-mysql/compose.yaml up -d'
            }
        }
        
    }
}