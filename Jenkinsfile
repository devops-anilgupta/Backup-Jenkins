pipeline {
    agent any

    stages {
        stage('SCP Copy File') {
            steps {
                script {
                    echo 'Copying file using SCP...'
                    
                    // Ensure the file exists before attempting to copy
                    sh '''
                        sudo su -
                        cd /root/.ssh
                        scp -o StrictHostKeyChecking=no ./* root@jenkins-slave:/home
                    '''
                }
            }
        }
    }
}
