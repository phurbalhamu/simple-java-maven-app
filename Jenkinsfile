pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

stage('Check-Git-Secrets') {
    steps {
        sh '''
            rm -f trufflehog || true
            trufflehog filesystem . --json --max-depth 50 > trufflehog.json
            cat trufflehog.json


        '''
    }
}
        

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }


        stage('Secure Copy To Server') {
            steps {
                sh '''
                    mkdir -p $WORKSPACE/jen
                    cp target/my-app-1.0-SNAPSHOT.jar $WORKSPACE/jen/
                '''
            }
        }
        

    }
}
