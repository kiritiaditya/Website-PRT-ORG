pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    agent {
        label 'k-m'
    }
    stages {
        stage('Git') {
            steps {
                git url: 'https://github.com/kiritiaditya/Website-PRT-ORG.git', branch: 'main'
            }
         }         
         stage('Docker') {
             steps {
                 sh 'sudo echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                 sh 'sudo docker build /home/ubuntu/jenkins/workspace/job1/ -t kiritiaditya/prt-task'
                 sh 'sudo docker push kiritiaditya/prt-task'
             }
         } 
         stage('K8s') {
             steps {
                 sh 'kubectl apply -f deploy.yaml'
                 sh 'kubectl apply -f service.yaml'
             }
         }
     } 
}
