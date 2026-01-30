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
        withCredentials([string(credentialsId: 'nvd-api-key', variable: 'NVD_API_KEY')]) {
            sh '''
            rm -rf dependency-check-report
            mkdir -p dependency-check-report
            chmod 777 dependency-check-report

            docker run --rm \
              -u root \
              -e NVD_API_KEY=${NVD_API_KEY} \
              -v "$(pwd):/src" \
              owasp/dependency-check \
              --scan /src \
              --format HTML \
              --out /src/dependency-check-report
            '''
        }
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
