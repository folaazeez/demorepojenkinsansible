pipeline {
    agent{
        label "ansible-node"
    }
    
    stages{
        stage ('Checkout Code'){
            steps{
                checkout scm
                }
            }
        stage ('Run Ansible Playbook'){
            steps{
                ansiblePlaybook(credentialsId: 'ansible-ssh', inventory: './inventory',playbook: 'ftp.yml')
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
    }
}
