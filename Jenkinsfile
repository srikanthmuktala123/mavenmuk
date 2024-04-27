pipeline {
    agent {
        docker {
            image 'docker pull maven:3.8.5-alpine'  // Replace with your desired Docker image
        }
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    git branch: 'main',
                       url: 'https://github.com/your-username/your-repo.git'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package' // Replace with your build command
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test' // Replace with your test command
            }
        }
        stage('Deploy') {  // Optional deploy stage using Docker image
            when {
                // Run only on successful builds (optional)
                expression { branch == 'master' && status == 'SUCCESS' }
            }
            steps {
                script {
                    def imageName = "maven:3.8.5-alpine"  // Replace with your image name
                        docker.build(imageName: imageName, '.')
                        docker.push(imageName)
                    }
                }
            }
        }
    }
}
}
