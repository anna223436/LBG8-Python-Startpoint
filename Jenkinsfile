pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh '''
                docker-compose build
                docker-compose push
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                ssh -i "~/.ssh/id_rsa" jenkins@34.88.190.72 << EOF
                rm -rf LBG8-Python-Startpoint
                git clone https://github.com/anna223436/LBG8-Python-Startpoint.git
                cd LBG8-Python-Startpoint
                docker-compose down
                docker-compose up -d
                '''
            }
        }
        stage('Clean Up') {
            steps {
                sh '''
                docker system prune --force
                ssh -i "~/.ssh/id_rsa" jenkins@34.88.190.72 << EOF
                docker system prune --force
                '''
            }
        }
    }
}
