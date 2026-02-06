pipeline {
    agent any
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
                    def inventory = "inventory/inven.ini"
                    def playbook = "playbooks/checks.yml"

                    echo "Inventory   : ${inventory}"
                    echo "Playbook    : ${playbook}"

                    bat """
                        wsl ansible-playbook \
                          -i ${inventory} \
                          ${playbook}
                    """
                }
            }
        }
    }

    post {
        success {
            echo "✅ MySQL installed and running successfully"
        }

        failure {
            echo "❌ MySQL install or health check failed"
        }

        always {
            cleanWs()
        }
    }
}
