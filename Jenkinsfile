pipeline {
    agent any

    stages {
        stage('SCP Copy File') {
            steps {
                script {
                    echo 'Copying file using SCP...'
                    
                    // Ensure the file exists before attempting to copy
                    sh '''
                        cd /
                        cd /home/ubuntu/temp
                        scp -o StrictHostKeyChecking=no ./* ubuntu@jenkins-slave:/home/temp
                    '''
                }
            }
        }
    }
}
