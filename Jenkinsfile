pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/employee-api'
        DB_URL = 'jdbc:postgresql://db:5432/employeedb'
        DB_USER = 'postgres'
        DB_PASSWORD = 'password'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/employee-management-api.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy to Server') {
            steps {
                sshagent(['server-ssh-key']) {
                    sh '''
                    ssh user@server "
                    docker pull $DOCKER_IMAGE &&
                    docker stop employee-api || true &&
                    docker rm employee-api || true &&
                    docker run -d --name employee-api -p 8080:8080 \
                    -e SPRING_DATASOURCE_URL=$DB_URL \
                    -e SPRING_DATASOURCE_USERNAME=$DB_USER \
                    -e SPRING_DATASOURCE_PASSWORD=$DB_PASSWORD \
                    $DOCKER_IMAGE
                    "
                    '''
                }
            }
        }
    }
}