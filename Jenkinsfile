pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "jay24666/retailapp"
        KUBE_NAMESPACE = "default"
    }

    stages {
        // stage('Clone Repo') {
        //     steps {
        //         git 'https://github.com/aws-containers/retail-store-sample-app.git'
        //     }
        // }

        stage('Build Docker Image') {
            steps {
                script {
                        //                     withDockerRegistry(credentialsId: 'dockerhub-creds', url: 'https://hub.docker.com/u/jay24666') {
                        //      sh "docker build -t ${IMAGE_NAME} ."// some block
                        // }
                      withDockerRegistry(credentialsId: 'dockerhub-creds'){
                    sh "docker build -t ${IMAGE_NAME} ."  // example for frontend
                      }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
               withDockerRegistry(credentialsId: 'dockerhub-creds') {
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        // stage('Deploy to Kubernetes') {
        //     steps {
        //         script {
        //             sh '''
        //             kubectl apply -f k8s/deployments/frontend-deployment.yaml
        //             kubectl apply -f k8s/services/frontend-service.yaml
        //             '''
        //         }
        //     }
        // }
    }
}
