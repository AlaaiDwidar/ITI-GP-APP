pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                docker build . -f dockerfile -t alaadwidar/final-image:v1.0 --network host
//                 sudo docker login -u ${USERNAME} -p ${PASSWORD}
//                 sudo docker push alaadwidar/final-image:v1.0
                """
                }
            }
        }
         stage('CD') {
            steps {
                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                kubectl apply -f /var/jenkins_home/workspace/Final-project-iti/deployment-app.yaml
                kubectl apply -f /var/jenkins_home/workspace/Final-project-iti/service-app.yaml
                """
                }
            }
        }
    }
}
