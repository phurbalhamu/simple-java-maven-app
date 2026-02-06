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

        
stage('Copy File') {
    steps {
        sh '''
            mkdir -p /home/bee/jen
            cp target/my-app-1.0-SNAPSHOT.jar /home/bee/jen/
        '''
    }
}



        
    }
}
