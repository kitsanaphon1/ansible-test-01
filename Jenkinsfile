pipeline {
    agent any

    environment {
        ANSIBLE_ENV = "${HOME}/ansible-azure-env"
    }

    stages {
        stage('Clone Ansible Repo') {
            steps {
                git branch: 'test', url: 'https://github.com/kitsanaphon1/ansible-test-01.git'
            }
        }

        stage('Run Ansible to Create VM') {
            steps {
                withCredentials([
                    string(credentialsId: 'azure-client-id', variable: 'AZURE_CLIENT_ID'),
                    string(credentialsId: 'azure-secret', variable: 'AZURE_SECRET'),
                    string(credentialsId: 'azure-tenant', variable: 'AZURE_TENANT'),
                    string(credentialsId: 'azure-subscription-id', variable: 'AZURE_SUBSCRIPTION_ID')
                ]) {
                    sh '''
                        source $ANSIBLE_ENV/bin/activate
                        ansible-playbook create-vm.yml
                    '''
                }
            }
        }
    }
}
