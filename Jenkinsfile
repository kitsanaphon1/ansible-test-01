pipeline {
    agent any

    environment {
        ANSIBLE_ENV = "/home/mis/ansible-azure-env"
        ANSIBLE_PLAYBOOK = "/home/mis/ansible-azure-env/bin/ansible-playbook"
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
                        export AZURE_CLIENT_ID=$AZURE_CLIENT_ID
                        export AZURE_SECRET=$AZURE_SECRET
                        export AZURE_TENANT=$AZURE_TENANT
                        export AZURE_SUBSCRIPTION_ID=$AZURE_SUBSCRIPTION_ID

                        $ANSIBLE_PLAYBOOK create-vm.yml
                    '''
                }
            }
        }
    }
}
