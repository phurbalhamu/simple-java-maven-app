pipeline {
    agent any

    stages {

        stage('Secret Scan') {
            steps {
                sh 'trufflehog filesystem .'
            }
        }


        
stage('SCA Scan') {
    steps {
        echo 'Running Source Composition Analysis using OWASP Dependency-Check (Docker)'
        sh '''
        docker run --rm \
          -v "$(pwd):/src" \
          owasp/dependency-check \
          --scan /src \
          --format HTML \
          --out /src/dependency-check-report
        '''
    }
}


        

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
