pipeline {
    agent any

    stages {

        stage('Secret Scan') {
            steps {
                sh 'trufflehog filesystem .'
            }
        }



stage('Source-Composition-Analysis') {
    steps {
        withCredentials([string(credentialsId: 'nvd-api-key', variable: 'NVD_API_KEY')]) {
            sh '''
            rm -f owasp*
            wget https://raw.githubusercontent.com/devopssecure/webapp/master/owasp-dependency-check.sh
            chmod +x owasp-dependency-check.sh

            export NVD_API_KEY=$NVD_API_KEY
            ./owasp-dependency-check.sh
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
