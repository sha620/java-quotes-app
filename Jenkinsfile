pipeline{
    agent any;
    stages{
        stage("code clone"){
          steps{
              git url :"https://github.com/sha620/java-quotes-app.git", branch:"master"
          }
        }
        stage("code build"){
            steps{
                sh "docker build -t java-app:la ."
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
               credentialsId: "new",
               usernameVariable: "user",
               passwordVariable: "pass"
               )]){
                   sh "docker login -u ${env.user} -p ${env.pass}"
                   sh "docker image tag java-app:la ${env.user}/java-app:la "
                   sh "docker push ${env.user}/java-app:la"
               }
            }
        }
        stage("code deploy"){
            steps{
                sh "docker run -d -p 80:80 java-app:la"
            }
        }
    }
}
