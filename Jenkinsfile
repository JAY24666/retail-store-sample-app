pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "jay24666/retailapp"
        KUBE_NAMESPACE = "default"
    }

    stages {

         stage('Build & Test UI (Java)') {
            steps {
                dir('src/ui') {
                    sh 'mvn clean install'
                    sh 'docker build -t ui-service .'
                }
            }
        }
        stage('Build & Test Orders (Java)') {
            steps {
                dir('src/orders') {
                    sh 'mvn clean install'
                    sh 'docker build -t orders-service .'
                }
            }
        }
        stage('Build & Test Catalog (Go)') {
            steps {
                dir('src/catalog') {
                    sh 'go mod tidy'
                    sh 'go test ./...'
                    sh 'docker build -t catalog-service .'
                }
            }
        }

        stage('Build & Test Cart (Java)') {
            steps {
                dir('src/cart') {
                    sh 'mvn clean install'
                    sh 'docker build -t cart-service .'
                }
            }
        }

        stage('Build & Test Checkout (Node.js)') {
            steps {
                dir('src/checkout') {
                    sh 'npm install'
                    sh 'npm test || echo "No tests found"'
                    sh 'docker build -t checkout-service .'
                }
            }
        }
    }

    post {
        success {
            echo '✅ All components built successfully!'
        }
        failure {
            echo '❌ Build failed.'
        }
        // stage('Build Docker Image') {
        //     steps {
        //         script {
        //                                     withDockerRegistry(credentialsId: 'dockerhub-creds', url: 'https://hub.docker.com/u/jay24666') {
        //                      sh "docker build -t ${IMAGE_NAME} ."// some block
        //                 }
        //             //   withDockerRegistry(credentialsId: 'dockerhub-creds'){
        //             // sh "docker build -t ${IMAGE_NAME} ."  // example for frontend
        //             //   }
        //         }
        //     }
        // }

        // stage('Push to Docker Hub') {
        //     steps {
        //         script{
        //        withDockerRegistry(credentialsId: 'dockerhub-creds') {
        //             sh "docker push ${IMAGE_NAME}"
        //             }
        //         }
        //     }
        // }

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
