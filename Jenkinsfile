pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'python-hello-world'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).inside {
                        sh 'pip install --no-cache-dir -r requirements.txt'
                        sh 'pytest test.py'
                    }
                }
            }
            post {
                success {
                    echo 'Las pruebas pasaron exitosamente.'
                }
                failure {
                    echo 'Las pruebas fallaron.'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image(DOCKER_IMAGE).run('-p 8000:8000')
                }
            }
        }
    }
}