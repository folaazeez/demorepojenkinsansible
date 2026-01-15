pipeline {
    agent{
        label "ansible-node"
    }
    
    stages{
        stage{
            steps{
                checkout scm
                }
            }
        stage{
            steps{
                ansiblePlaybook{
                    credentialsId: 'ssh_user',
                    inventory: './inventory',
                    playbook: 'ftp.yml'
                }
            }
        }
    }
}
