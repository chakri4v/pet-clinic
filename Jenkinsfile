pipeline{
    agent any
            environ
        stages{

            stage('Build'){
                steps{
                    sh 'docker build -t chakri4v/pet-clinic:1.0.0 -f Docker-multistage .'
                    sh 'docker run -d -p 8080:8080 --name spring-pet chakri4v/pet-clinic:1.0.0'
                    sh 'sleep 2'
                    sh "container=`docker ps | grep spring-pet | awk '{print ${1}}'`"
                    sh "docker stop $container"
                    sh "stopped=`docker ps -a| grep spring-pet | awk '{print ${1}}'`"
                    sh "docker rm $stopped"
                    sh "image=`docker images | grep spring-pet | awk '{print ${3}}'`"
                    sh "docker rmi $image"

                // providing docker credentials
                
                    withCredentials([
                        usernamePassword(credentials:'DockerHub' , usernameVariable: USER, passwordVariable: PASS)
                    ])
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh "docker push chakri4v/pet-clinic:1.0.0"

                }
            }
        }


}
