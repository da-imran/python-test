pipeline {
    agent any
    triggers {
        pollSCM '*/5 * * * *'
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                cd /var/jenkins_home/jobs/python-test/workspace
                docker compose up -d
                '''
            }
        }
        stage('Test') {
            steps {
                sh '''
                python3 -V
                apt update
                apt install -y python3 python3-pip python3-venv
                . /venv/bin/activate
                pip install pytest selenium
                docker compose up -d
                sleep 20
                python test_devopstest.py
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