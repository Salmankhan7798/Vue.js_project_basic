pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                sh 'npm install'
                sh 'npm run test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook all nginx_setup.yml'
                sh 'cp ansible/vue-app.conf /etc/nginx/sites-available/'
                sh 'ln -s /etc/nginx/sites-available/vue-app.conf /etc/nginx/sites-enabled/'
                sh 'systemctl restart nginx'
            }
        }
    }
}  
