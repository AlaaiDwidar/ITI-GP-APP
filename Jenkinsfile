pipeline {
    agent any

    stages {
        stage('CI') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                docker build . -f dockerfile -t alaadwidar/final-image:v1.0 --network host
//              docker login -u $USERNAME -p $PASSWORD
//              docker push alaadwidar/final-image:v1.0

                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
               
                """
                }
            }
        }
         stage('CD') {
            steps {
                git 'https://github.com/AlaaiDwidar/ITI-GP-APP.git'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                kubectl apply -f /var/jenkins_home/workspace/deployment-app.yaml
                kubectl apply -f /var/jenkins_home/workspace/service-app.yaml
                """
                }
            }
        }
    }
}
