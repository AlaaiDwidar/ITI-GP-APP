pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                
                
                
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker build . -f dockerfile -t alaadwidar/final-image:v1.0 --network host

                docker push alaadwidar/final-image:v1.0

               
                """
                }
            }
        }
         stage('CD') {
            steps {
                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                kubectl create namespace app
             
                kubectl apply -f /var/jenkins_home/workspace/Final-project-iti/deployment-app.yaml -n app

                kubectl apply -f /var/jenkins_home/workspace/Final-project-iti/service-app.yaml -n app

                """
                }
            }
        }
    }
}
