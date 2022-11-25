pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker-compose build
                '''

            }
        }
        stage('Push') {
            steps {
                sh '''
                docker-compose push
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                ssh -i "~/.ssh/id_rsa" jenkins@34.155.152.33 << EOF
                rm -rf LBG8-Python-Startpoint
                git clone https://github.com/anna223436/LBG8-Python-Startpoint.git
                cd LBG8-Python-Startpoint
                docker-compose down
                docker-compose up -d

                '''
            }
        }
    }
}
