pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    def inventory = "Ansible/Inventory/inventory.ini"
                    def playbook  = "Ansible/Playbooks/checks.yaml"

                    echo "Inventory : ${inventory}"
                    echo "Playbook  : ${playbook}"

                    bat """
                        wsl ansible-playbook ^
                          -i ${inventory} ^
                          ${playbook}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ Ansible playbook ran successfully"
        }
        failure {
            echo "❌ Ansible playbook failed"
        }
        always {
            cleanWs()
        }
    }
}
