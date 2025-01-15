pipeline {
    agent { label "docker" }

    stages {
        stage("Code Clone from GitHub") {
            steps {
                echo "Cloning repository from GitHub..."
                git url: "https://github.com/mohitlavania07/my-dir.git", branch: "main"
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying using Docker Compose..."
                sh """
                    docker-compose down || true
                    docker-compose up -d --build
                """
            }
        }

        stage("Push to Dockerhub") {
            steps {
                echo "Pushing the image to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: "docker-cred", passwordVariable: 'dockerPass', usernameVariable: 'dockerUser')]) {
                    sh """
                        docker login -u ${dockerUser} -p ${dockerPass}
                        docker image tag wanderlust-ci-cd_frontend ${dockerUser}/wanderlust
                        docker push ${dockerUser}/wanderlust
                    """
                }
            }
        }
    }
}
