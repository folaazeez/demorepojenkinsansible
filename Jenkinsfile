pipeline {
    agent{
        label "ansible-node"
    }
    parameters {
        choice(name: 'action',  choices: ['install', 'uninstall'], description: 'Select the action to perform')    
    }
    stages{
        stage ('Checkout Code'){
            steps{
                checkout scm
            }
        }
        stage ('Run Install Playbook '){
            when {
                expression { params.action == 'install' }
            }
            steps{
                ansiblePlaybook(credentialsId: 'ansible-ssh', inventory: './inventory',playbook: 'ftp-install.yml')
            }
        }
        stage ('Run Uninstall Playbook'){            
            when {
                expression { params.action == 'uninstall' }
            }
            steps{
                ansiblePlaybook(credentialsId: 'ansible-ssh', inventory: './inventory',playbook: 'ftp-uninstall.yml')
            }
        }        
    }

    post{
        always{
            archiveArtifacts '*.log'
        }
        success{
            echo 'Playbook executed successfully'
        }
        failure{
            echo 'Playbook failed to execute!'
        }
        cleanup { cleanWs() }

    }

}
