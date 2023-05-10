pipeline{
    agent any
        stages{

            stage('Build'){
                steps{
                    sh 'docker build -t chakri4v/jenkins:1.0.0 -f Docker-multistage .'
                }
            }
        }


}
