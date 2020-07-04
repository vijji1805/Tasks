pipeline {
    agent any

    environment {
    VERSION ="1.${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build Image') {
            steps {
                script {
                    echo "My Image is ${VERSION}"
                    sh 'docker build -t vijayavadlamudi/php-hello:${VERSION} .'    
                }
                
            }
        }
        
        stage('Push Image') {
            steps {
               withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'REGISTRY_PWD', usernameVariable: 'REGISTRY_USER')]) {
                    sh 'docker login -u=$REGISTRY_USER -p=$REGISTRY_PWD'    
                    sh 'docker push vijayavadlamudi/php-hello:${VERSION}'
                    sh 'docker service update --image vijayavadlamudi/php-hello:${VERSION} php-hello'
                }
            }
        }
    }
}
