pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    // Ensure the local directory exists before proceeding
                    sh '''
                    whoami
                    if [ ! -d /home/ubuntu/temp ]; then
                        sudo mkdir -p /home/ubuntu/temp
                    fi
                    '''
                }
            }
        }

        stage('Copy Files via SCP') {
            steps {
                script {
                    echo 'Copying files using SCP...'

                    // Check if there are files in the directory and copy them via SCP
                    sh '''
                    whoami
                    cd /home/ubuntu/temp
                    if [ "$(ls -A .)" ]; then
                        scp -o StrictHostKeyChecking=no ./* ubuntu@jenkins-slave:/home/temp || echo "SCP failed. Please check the connection or path."
                    else
                        echo "No files to copy."
                    fi
                    '''
                }
            }
        }
    }
}
