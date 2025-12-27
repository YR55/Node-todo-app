pipeline{
    agent any
    stages{
        stage('Code'){
            steps{
                echo "cloning the code from github"
                git url: 'https://github.com/YR55/node-todo-cicd.git/', branch: 'master'
            }
        }
        stage('Build'){
            steps{
                sh 'docker build . -t yogeshverma08/node-todo-test:latest'
            }
            
        }
         stage('Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPassword')])
                {
                    
                      sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                      sh 'docker push yogeshverma08/node-todo-test:latest'
                }
            }
            
        }
        stage('Test'){
            steps{
                echo "testing perform"
                echo "Running unit tests from test.js"
        sh 'npm install'  // Install dependencies
        sh 'npm test' // Run the test file directly
            }
            
        }
        stage('Deploy'){
            steps{
                echo "deploying on production server"
                sh 'docker compose down && docker compose up -d'
            }
        }
    }
}
