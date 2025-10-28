pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t mypythonflaskapp ."
            }
        }

        stage('Run') {
            steps {
                echo "Run application in Docker Container"

                // forcibly removes the Docker container named mycontainer.
                // If the container does not exist, this command will fail and return an error,
                // but 'exit 0' tells the shell to exit with a success status.
                bat "docker rm -f mycontainer || exit 0"

                // Run the container in detached mode (-d) so it runs in the background.
                // Without -d, the terminal shows logs and gets blocked by the container process.
                bat "docker run -d -p 5000:5000 --name mycontainer mypythonflaskapp"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
