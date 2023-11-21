pipeline {
    agent any
    environment {YOUR_NAME = credentials("YOUR_NAME")}
    stages {
        stage('Build') {
            steps {
                sh '''
                docker build -t hughston05/task1-nginx nginx .
                '''
            }

        }
        stage('Push') {
            steps {
                sh '''
                docker push hughston05/task1-nginx
                '''
            }

        }
        stage('Deploy') {
            steps {
                sh '''
                ssh jenkins@hugh-deploy <<EOF
                export YOUR_NAME = ${YOUR_NAME}
                docker network rm task1-net && echo "task1net removed" || echo "task1-net does not exist"
                docker network create task1-net
                docker stop task1-nginx && echo "stopped nginx" || echo " nginx is not running"
                docker rm task1-nginx && each "removed nginx" || echo "nginx does ot exist"
                docker stop flask-app && echo "stopped flaskapp" || echo " flaskapp is not running"
                docker rm flask-app && each "removed flaskapp" || echo "flaskapp does ot exist"
                docker run - d --name nginx --network task1-net -p 80:80 hughston05/task1-jenk
                docker run -d --name flask-app --network task1-net hughston05/task1-jenk
                '''
            }

        }

    }

}

