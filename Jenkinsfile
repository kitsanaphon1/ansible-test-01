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
                    string(credentialsId: 'AZURE_CLIENT_ID', variable: 'AZURE_CLIENT_ID'),
                    string(credentialsId: 'AZURE_SECRET', variable: 'AZURE_SECRET'),
                    string(credentialsId: 'AZURE_TENANT', variable: 'AZURE_TENANT'),
                    string(credentialsId: 'AZURE_SUBSCRIPTION_ID', variable: 'AZURE_SUBSCRIPTION_ID')
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
