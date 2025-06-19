pipeline {
    agent { 
        label 'VM agent'
    }

    environment {
        IMAGE = 'mon-image'
        CONTENEUR = 'mon-conteneur'
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo "Création de l'image Docker: ${IMAGE}"
                    sh "docker build -t ${IMAGE} ."
                }
            }
        }

        
        stage('Stop') {
            steps {
                script {
                    echo "Arrêt du conteneur"
                    sh "docker stop ${CONTENEUR} || true"
                }
            }
        }

        stage('Suppr') {
            steps {
                script {
                    echo "Suppression du conteneur"
                    sh "docker rm ${CONTENEUR} || true"
                }
            }
        }

        stage('Demarre') {
            steps {
                script {
                    echo "Démarrage du conteneur depuis ${IMAGE}"
                    sh "docker run -d --name ${CONTENEUR} -p 9000:80 ${IMAGE}"
                }
            }
        }

         stage('Copier fichier HTML') {
            steps {
                script {
                    sh 'sudo cp index.html /var/www/html/'
                }
            }
        }

        stage('Redémarrer Apache') {
            steps {
                script {
                    sh 'sudo systemctl restart apache2'
                }
            }
        }
    
    }
}
