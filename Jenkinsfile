pipeline {
    agent any

    tools {
        // Specify the JDK version
        jdk 'JDK11'
    }

    environment {
        NODE_VERSION = '18.20.3'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the repository
                checkout scm
            }
        }

        stage('Setup Node') {
            steps {
                // Install the specified Node.js version using nvm
                sh '''
                . ~/.nvm/nvm.sh
                nvm install ${NODE_VERSION}
                nvm use ${NODE_VERSION}
                '''
            }
        }

        stage('Clean') {
            steps {
                // Clean node_modules and yarn cache
                sh '''
                rm -rf client-app/node_modules
                yarn cache clean
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install dependencies
                    dir('client-app') {
                        sh 'yarn install'
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Run the Gradle build command
                    sh './gradlew clean build'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run the Gradle test command
                    sh './gradlew test'
                }
            }
        }
    }

    post {
        always {
            // Publish test results to Jenkins
            junit '**/build/test-results/test/*.xml'
            
            // Archive build artifacts, if any
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
    }
}
