pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Replace with your build command
                    sh './gradlew build'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Replace with your test command
                    sh './gradlew test'
                }
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml'
            archiveArtifacts artifacts: '**/build/libs/*.jar', allowEmptyArchive: true
        }
        failure {
            mail to: 'team@yourcompany.com',
                 subject: "Build failed in Jenkins: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                 body: "Something is wrong with ${env.JOB_NAME} #${env.BUILD_NUMBER}. Please fix it."
        }
    }
}
