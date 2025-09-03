pipeline{
    agent any;
    stages{
        stage("code clone"){
            steps{
                git url: "https://github.com/sha620/java-quotes-app.git",branch: "master"
            }
        }
        stage("code build"){
          steps{
              sh "docker build -t java-app:latest ." 
              
          } 
        }
        stage("code test"){
            steps{
                echo "test"
            }
        }
        stage("code push to docker hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"peda",
                usernameVariable: "user",
                passwordVariable:"pass"
                )]){
                sh "docker login -u ${env.user} -p ${env.pass}"
                sh "docker image tag java-app:latest ${env.user}/java-app:latest"
                sh "docker push ${env.user}/java-app:latest"
                }
            }
            
        }
        stage("code deploy"){
            steps{
                sh "docker run -d java-app:latest"
            }
            
        }
    }
}
