pipeline {
    environment {
        DOCKERHUB_CREDENTIALS = credentials("docker")
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
        stage('Docker') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker build -t kiritiaditya/prt-task .
                        docker push kiritiaditya/prt-task
                    '''
                }
            }
        }
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
