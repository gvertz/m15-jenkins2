pipeline {
    agent any

    stages {
        stage('Build Image') {
            steps {
                script {
                    // Paso a) Construcción de la imagen
                    docker.build 'mi-imagen:latest'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Paso b) Ejecución de un contenedor usando esa imagen
                    docker.image('mi-imagen:latest').run('-p 8080:8080 --name mi-contenedor')
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    // Paso c) Subir esa imagen a un repositorio de imágenes
                    docker.withRegistry('https://registry.example.com', 'mi-credencial') {
                        docker.image('mi-imagen:latest').push()
                    }
                }
            }
        }
    }

    post {
        always {
            // Limpieza: detener y eliminar el contenedor después de ejecutar el pipeline
            script {
                docker.image('mi-imagen:latest').stop()
                docker.image('mi-imagen:latest').remove()
            }
        }
    }
}
