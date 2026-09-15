pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out project'
            }
        }

        stage('Test') {
            steps {
                sh '''
                    python3 -m py_compile app/app.py
                '''
            }
        }

        stage('Build and Deploy') {
            steps {
                sh '''
                    cd ansible
                    ansible-playbook -i inventory.ini deploy.yml
                '''
            }
        }

        stage('Verify') {
            steps {
                sh '''
                    kubectl get nodes
                    kubectl get pods
                    kubectl get services
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD pipeline failed.'
        }
    }
}
