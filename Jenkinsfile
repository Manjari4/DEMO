pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                sh '''
                    ansible-playbook \
                    -i Ansible/Inventory/inventory.ini \
                    Ansible/Playbooks/checks.yaml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Ansible playbook executed successfully'
        }
        failure {
            echo '❌ Ansible playbook execution failed'
        }
    }
}
