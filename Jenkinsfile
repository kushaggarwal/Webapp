pipeline{
    agent any
    options{
        buildDiscarder(logRotator(numToKeepStr:'5'))
    }
    environment{
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages{
        stage('Build'){
            steps{
                echo "Building an docker image for our web application"
                sh 'docker build -t kushaggarwal/nodejs-app .'
            }
        }
        stage('Login'){
            steps{
                echo "Logging into dockerhub account"
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push'){
            steps{
                echo "Pushing the docker image to registary"
                sh "docker push kushaggarwal/nodejs-app"
            }
        }
        stage('Run the docker images'){
            steps{
                echo "Running the docker image"
                sh "docker run -d -p 8000:3000 kushaggarwal/nodejs-app"
            }
        }
    }
}