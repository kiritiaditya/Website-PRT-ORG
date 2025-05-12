pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials("f42f667f-e6b4-49e3-a56f-f5b294d45693")
    }
    agent {
        label ''
    }
    stages {
        stage('Git') {
            steps {
                git url: 'https://github.com/kiritiaditya/Website-PRT-ORG.git', branch: 'main'
            }
         }         
         stage('Docker') {
             steps {
                 sh 'sudo docker login -u $(DOCKERHUB_CREDENTIALS_USR) -p $(DOCKERHUB_CREDENTIALS_PSW)'
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
