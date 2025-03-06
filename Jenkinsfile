    pipeline {
        agent any  // Use any available Jenkins agent

        environment {
            IMAGE_NAME = "your-dockerhub-username/your-app"
            IMAGE_TAG = "latest"
        }

        stages {
            stage('Checkout Code') {
                steps {
                    git branch: 'master', url: 'https://github.com/ramishshakeel1/Mlops-CI-CD.git'
                }
            }

            stage('Build Docker Image') {
                steps {
                    script {
                        sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
                    }
                }
            }

            stage('Push to Docker Hub') {
                steps {
                    script {
                        // Use withCredentials to securely bind Docker Hub credentials
                        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: '21i1363', passwordVariable: '@Goblin.1')]) {
                            // Log in to Docker Hub
                            sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                            
                            // Push the Docker image to Docker Hub
                            sh 'docker push $IMAGE_NAME:$IMAGE_TAG'
                        }
                    }
                }
            }


            stage('Deploy') {
                steps {
                    script {
                        sh 'docker run -d -p 5000:5000 $IMAGE_NAME:$IMAGE_TAG'
                    }
                }
            }
        }
    }
