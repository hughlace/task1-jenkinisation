pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t hughston05/task1-jenk .
                '''
            }

        }
        stage('Push') {
            steps {
                sh '''
                docker push hughston05/task1-jenk
                '''
            }

        }
        stage('Deploy') {
            steps {
                sh '''
                docker stop task1
                docker rm task1
                docker run -d -p 80:5500 --name task1 hughston05/task-1jenk
                '''
            }

        }

    }

}

