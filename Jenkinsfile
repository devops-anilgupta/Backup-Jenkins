pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    // Ensure the directory exists before proceeding
                    sh '''
                    if [ ! -d /home/ubuntu/temp ]; then
                        mkdir -p /home/ubuntu/temp
                    fi
                    '''
                }
            }
        }

        stage('Copy Files via SCP') {
            steps {
                script {
                    echo 'Copying files using SCP...'

                    // Ensure SCP command is executed safely with no host key checking
                    sh '''
                    cd /home/ubuntu/temp
                    if [ "$(ls -A .)" ]; then
                        scp -o StrictHostKeyChecking=no ./* ubuntu@jenkins-slave:/home/temp
                    else
                        echo "No files to copy."
                    fi
                    '''
                }
            }
        }
    }
}
