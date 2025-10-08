pipeline{
    agent any;
    stages{
        stage(clone){
            steps{
                git url:"https://github.com/sha620/java-quotes-app",branch:"master"
            }
        }
        stage(build){
            steps{
                sh "docker build -t java-app:ll ."
            }
        }
        stage(test){
            steps{
                echo "test"
            }
        }
        stage(push){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "papa",
                    usernameVariable: "user",
                    passwordVariable:"pass"
                    )]){
                        sh "docker login -u ${env.user} -p ${env.pass}"
                        sh "docker image tag java-app:ll ${env.user}/java-app:ll"
                        sh "docker push ${env.user}/java-app:ll"
                    }
            }
        }
        stage(deploy){
            steps{
                sh "docker stop java && docker rm java"
                sh "docker run -d --name java java-app:ll"
            }
        }
    }
}
