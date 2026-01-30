pipeline {
    agent any

    stage('Secret Scan') {
    steps {
        sh 'trufflehog filesystem .'
    }
}
    
    stages {
        stage('Build') {
            steps {
                echo 'Building the project'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests'
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application'
            }
        }
    }
}
