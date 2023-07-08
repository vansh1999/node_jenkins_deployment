
pipeline {
    agent {label 'stage'}
    stages{
        
        stage("Code Clone"){
            steps{
                git url: 'https://github.com/vansh1999/node_jenkins_deployment.git' , branch : 'master'
            }
        }
        
        stage("Build and test"){
            steps{
                sh "docker build . -t vansh1999/nodeapp:latest"
            }
        }
        
        stage("Login and push Image"){
            steps{
                echo "loggin into dockerhub"
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
                    
                }
                sh "docker push vansh1999/nodeapp:latest"

            }
        }
        
        stage("Deploy"){
            steps{
                sh "docker-compose down"
                sh "docker-compose up -d"
            }
        }
    }
}
