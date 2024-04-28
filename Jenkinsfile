pipeline {
    agent any

    stages {
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
