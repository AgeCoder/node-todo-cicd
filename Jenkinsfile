@Library("sharedlib") _

pipeline {
    agent { label "age" }  // Make sure 'age' is a valid agent label

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()  // This should be defined in your shared library
                }
            }
        }

        stage('Code') {
            steps {
                script {
                    clone("https://github.com/AgeCoder/node-todo-cicd.git", "master")  // Assuming clone() is from your shared lib
                }
            }
        }

        stage('Build') {
            steps {
                echo 'Building the code'
                script {
                    docker_build("notes-app", "latest", "aligthage")  // docker_build() should also be part of the shared library
                }
            }
        }

        stage('Push') {
            steps {
                echo 'Pushing the Image to Docker Hub'
                script {
                    docker_push("notes-app", "latest", "aligthage")  // Ensure docker_push() handles Docker login and push
                }
                echo 'Image pushed successfully'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the code'
                sh "docker compose up -d"
                echo 'Deployment completed successfully'
            }
        }
    }
}
