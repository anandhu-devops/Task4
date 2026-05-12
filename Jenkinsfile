pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Test') {
            steps {
                sh '''
                    docker rm -f myapp_test || true
                    docker run -d --name myapp_test -p 8080:8080 myapp:latest
                    sleep 5
                    docker ps | grep myapp_test
                '''
            }
        }
    }

    post {
        always {
            sh 'docker rm -f myapp_test || true'
        }
    }
}
