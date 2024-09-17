pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out git repo'
                git url: 'https://gitea.dev.MYDOMAIN.com/MYORG/MYREPO.git'
            }
        }
        
        stage('Build') {
            steps {
                echo 'Building the project...'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['jenkins-deployment-ssh-id']) {
                    script {
                        sh '''
                        scp -o StrictHostKeyChecking=no -P 2223 index.html jenkins@timesheet.MYDOMAIN.com:/www/apps/timesheet/
                        '''
                    }
                    echo 'Deployed index.html to remote host via SSH using Jenkins credentials.'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
