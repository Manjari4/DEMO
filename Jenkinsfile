pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Install MySQL') {
            steps {
                sh '''
                    ansible-playbook \
                    -i Ansible/Inventory/inventory.ini \
                    Ansible/Playbooks/checks.yaml \
                    --tags install
                '''
            }
        }

        stage('Start MySQL Service') {
            steps {
                sh '''
                    ansible-playbook \
                    -i Ansible/Inventory/inventory.ini \
                    Ansible/Playbooks/checks.yaml \
                    --tags service
                '''
            }
        }

        stage('Check MySQL Service') {
            steps {
                sh '''
                    ansible-playbook \
                    -i Ansible/Inventory/inventory.ini \
                    Ansible/Playbooks/checks.yaml \
                    --tags check
                '''
            }
        }
    }

    post {
        success {
            echo '✅ MySQL pipeline completed successfully'
        }
        failure {
            echo '❌ MySQL pipeline failed'
        }
    }
}
