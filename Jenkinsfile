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

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        
stage('Secure Copy') {
    steps {
        sshagent(['tomcat']) {
            sh '''
                scp -o StrictHostKeyChecking=no \
                target/my-app-1.0-SNAPSHOT.jar \
                ubuntu@54.245.203.229:/tmp/
            '''
        }
    }
}

        
    }
}
