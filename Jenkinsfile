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
        stage("deploy the App"){
            steps{
                echo "Deploy App with docker compose"
                sh "docker compose down || true"
                sh "docker compose up -d --build"
            }
        }
    }
}
