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
            rm trufflehog || true
            docker run gesellix/trufflehog --json https://github.com/cehkunal/webapp.git > trufflehog
            cat trufflehog
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
