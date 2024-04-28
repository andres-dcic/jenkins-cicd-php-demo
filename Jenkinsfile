pipeline {
    agent any

    stages {
        stage('Initialize') {
            steps {
                sh '''
                    echo "PATH= $(PATH)"
                '''
                }
            }

    
        stage('Ceck-Git-Secrets') {
            steps {
                sh 'rm trufflehog || true'
                sh 'docker run rajlocuz/trufflehog  --json https://github.com/andres-dcic/jenkins-cicd-php-demo.git > trufflehog'
                sh 'cat trufflehog'
                
                }
            }

        
        stage('test deploy') {
            steps {
                echo 'Hello World'
                sh 'touch prueba.txt'
                sshagent(['ssh-mv']){
                    sh 'scp -o StrictHostKeyChecking=no  index.html andres@192.168.0.143:/var/www/html'
                }
            }
        }
    }
}
