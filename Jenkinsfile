pipeline{
    agent any
    
    stages{
        stage("Code clone"){
            steps{
                echo " Clone the code from Github"
                git url: "https://github.com/Sangeeta-cmd/two-tier-flask-app.git", branch: "main"
            }
        }
        stage("build image"){
            steps{
                echo " Build the doker image "
                sh "docker build -t flask-app:latest ."
            }
        }
        stage("Push to Dockerhub"){
            steps{
                echo "Push Image to DockerHub"
                withCredentials([usernamePassword(
                    credentialsId: "DockerHubCred", 
                    usernameVariable: "dockerHubUser", 
                    passwordVariable: "dockerHubPass"
                    )]){
                        sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                        sh "docker image tag flask-app:latest ${env.dockerHubUser}/flask-app:v1"
                        sh "docker push ${env.dockerHubUser}/flask-app:v1"
                }
                echo "DOcker Push Successful!"
            }
        }
        stage("deploy the App"){
            steps{
                echo "Deploy App with docker compose"
                sh "docker compose down || true"
                sh "docker compose up -d --build"
            }
        }
    }
}
