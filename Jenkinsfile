pipeline {
    agent any
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                docker compose up -d
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                python3 -V
                apt update -y
                apt upgrade -y
                apt install -y python3 python3-pip python3-venv
                . /venv/bin/activate
                pip install pytest selenium
                docker compose up -d
                sleep 20
                python3 test_devopstest.py
                '''
            }
        }
        stage('Deliver') {
            steps {
                sh '''
                echo "Ready to deliver"
                '''
            }
        }
    }
}