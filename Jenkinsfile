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
                    credentialsId: 'ansible-ssh',
                    inventory: './inventory',
                    playbook: 'ftp.yml'
                }
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
