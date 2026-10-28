pipeline{
    agent any

    environment{
        DOCKER_IMAGE = 'ajaykumar2602/myapp3'
        DOCKER_TAG = 'v1'
    }

    stage{
        stage('Clone Repository'){
            steps{
                git branch:'main', url: 'https://github.com/Ajay00-07/exp4.git'
            }
        }

        stage('Build Docker Image'){
            steps{
                bat 'docker build -t %DOCKER_IMAGE%:%DOCKER_TAG% .'
            }
        }

        stage('Docker Login'){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: 'Dockerhub',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]){
                    bat 'echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin'
                }
            }
        }

        stage('push Docker Image'){
            steps{
                bat 'docker push %DOCKER_IMAGE%:%DOCKER_TAG%'
            }
        }
    }

    post{
        success{
            echo 'Docker image pushed successfully!'
        }
        failure{
            echo 'Failed to push Docker image!'
        }
    }
}
