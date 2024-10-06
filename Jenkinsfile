pipeline{
    agent {label "neeraj"}
    
    stages{
        stage("Code"){
            steps{
                echo "Cloning the Code"
                git url:"https://github.com/neeraj-gs/django-notes-app.git",branch:"main"
                echo "Code Cloning successfull"
            }
            
        }
        stage("Build"){
            steps{
                echo "Building the Code"
                sh "docker build -t notes-app:latest ."
            }
        }
        stage("Test"){
            steps{
                echo "Testing the Code"
            }
        }
        stage("Push to Docker Hub"){
            steps{
                echo "Pushinf image to docker hu"
                withCredentials([usernamePassword('credentialsId':"dockerHubCred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag notes-app:latest neerajgs/notes-app:latest"
                    sh "docker push neerajgs/notes-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploying the Code"
                sh "docker compose up -d"
            }
        }
    }
}
