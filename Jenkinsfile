pipeline {
    agent {
        label 'ubuntu-agent1'
    }
    environment {
        SUDO_PASSWORD = credentials('agent1-sudo-password-id')
    }

    stages {
        stage('Install Apache') {
            steps {
                sh '''
                echo "$SUDO_PASSWORD" | sudo -S apt update
                echo "$SUDO_PASSWORD" | sudo -S apt install -y apache2
                '''
            }
        }
        stage('Verify Apache Installation') {
            steps {
                sh '''
                apache2 -v
                curl http://127.0.0.1/test1.html
                curl http://127.0.0.1/index.php
                '''
            }
        }
        stage('Check Logs') {
            steps {
                sh '''
                grep -E "(4[0-9]{2}|5[0-9]{2})" /var/log/apache2/access.log
                '''
            }
        }
    }
}
