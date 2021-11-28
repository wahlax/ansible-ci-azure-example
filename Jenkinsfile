pipeline {
    agent any

    environment {
        PATH                 = "${env.PATH}:~/.local/bin/"
        LOCAL_AZURE_CLIENT_ID  = credentials('azure-client-id')
        LOCAL_AZURE_CLIENT_SECRET  = credentials('azure-client-secret')
        LOCAL_AZURE_SUBSCRIPTION_ID  = credentials('azure-subscription-id')
        LOCAL_AZURE_TENANT_ID  = credentials('azure-tenant-id')
    }

    stages {
        stage('Provision') {
            steps {
                sh 'ansible-galaxy install -r requirements.yml'
                sh '''
                  source ./terraform-env.shl
                  terraform init -input=false
                  terraform plan -out=tfplan -input=false
                  terraform apply -input=false tfplan
                '''
            }
        }
    }
}
