pipeline {
    agent { label "Dev-agent" }
    
    stages {
        stage("Clone Code") {
            steps {
                echo "Cloning the code"
                git url: "https://github.com/Mehboob1129/node-todo-cicd-with-jenkins.git", branch: "master"
            }
        }

        stage("Building") {
            steps {
                echo "Building the image"
                sh "sudo docker build -t node-todo-cicd-with-jenkins ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                echo "Pushing the image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "sudo docker tag node-todo-cicd-with-jenkins ${env.dockerHubUser}/node-todo-cicd-with-jenkins:latest"
                sh "sudo docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "sudo docker push ${env.dockerHubUser}/node-todo-cicd-with-jenkins:latest"
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the container"
                sh "sudo docker run -d -p 8000:8000 mehboob1129/node-todo-cicd-with-jenkins:latest"
            }
        }
    }
}
