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
                sh 'docker run rajlocuz/trufflehog  --json https://github.com/andres-dcic/jenkins-cicd-php-demo.git > trufflehog.json'
                        script {
                        def jsonReport = readFile('trufflehog.json')
                        def htmlReport = """
                            <html>
                            <head>
                                <title>Trufflehog Scan Report</title>
                            </head>
                            <body>
                                <h1>Trufflehog Scan Report</h1>
                                <pre>${jsonReport}</pre>
                            </body>
                            </html>
                            """
                            writeFile file: 'scanresults/trufflehog-report.html', text: htmlReport
                 
                
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
