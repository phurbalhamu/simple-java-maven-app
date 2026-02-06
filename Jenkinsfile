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

        
stage('secure copy Deploy-To-Tomcat') {
    steps {
        sshagent(['tomcat']) {
            sh '''
                scp -o StrictHostKeyChecking=no \
                target/*.war \
                ubuntu@54.245.203.229:/tmp/apache-tomcat-8.5.38/webapps/
            '''
        }
    }
}
        
    }
}
