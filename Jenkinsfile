pipeline{
    agent any;
    stages{
        stage("clone"){
            steps{
                git url :"https://github.com/sha620/java-quotes-app.git", branch: "master"
                
            }
        }
        stage("build"){
            steps{
                sh "docker build -t java-app:latest ."
            }
            
        }
        stage("test"){
            steps{
                echo "test"
            }
            
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(
                credentialsId: "mom",
                usernameVariable: "user",
                passwordVariable: "pass"
                )]){
                sh "docker login -u ${env.user} -p ${env.pass}"
                sh "docker image tag java-app:latest ${env.user}/java-app:latest"
                sh "docker push ${env.user}/java-app:latest"
                }
            }
            
        }
        stage("deploy"){
            steps{
                sh "docker run -d java-app:latest" 
                }
            
        }
        
    }
}
