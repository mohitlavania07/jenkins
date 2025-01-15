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
                    # Ensure the Jenkins user has permissions for Docker
                    docker-compose down || true
                    docker-compose up -d --build
                """
            }
        }
    }
}
