pipeline {
    agent none
    
    environment {
        ANSIBLE_INVENTORY = "/etc/ansible/hosts"
        ANSIBLE_PLAYBOOK = "assignment1.yml"
        ANSIBLE_VAULT_PASSWORD_FILE = "/etc/ansible/vault_pass.txt"
        SSH_PRIVATE_KEY = '/var/lib/jenkins/.ssh/id_rsa'
    }

    stages {
    
        stage('Run Ansible Playbook') {
            agent { label 'master' }
            steps {
                script {
                    sh """
                        ansible-playbook ${ANSIBLE_PLAYBOOK} -i ${ANSIBLE_INVENTORY} --private-key=${SSH_PRIVATE_KEY} --vault-password-file ${ANSIBLE_VAULT_PASSWORD_FILE}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Ansible Playbook executed successfully!'
        }
        failure {
            echo 'Ansible Playbook failed to execute.'
        }
    }
}
