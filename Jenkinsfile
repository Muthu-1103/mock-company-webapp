pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // TODO: Build step
                sh './gradlew assemble'
            }
        }
        stage('Test') {
            steps {
                // TODO: Test step
                sh './gradlew test'
            }
        }
    }
}
