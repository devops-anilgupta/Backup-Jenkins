pipeline {
    agent any

    stages {
        stage('Prepare Environment') {
            steps {
                script {
                    // Ensure the local directory exists before proceeding
                    sh '''
                    whoami
                    if [ ! -d /home/jenkins/temp ]; then
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
                        #!/bin/bash
                        set -e  # Exit on error
                        exec > script.log 2>&1  # Redirect output and errors to log file
                        
                        whoami
                        cd /
                        cd /home/temp
                        
                        
                        # Compress the folder with sudo and log if password prompt is an issue
                        echo "Compressing the file..."
                        tar -czvf jenkins-file.tar.gz /var/lib/jenkins
                        echo "File has been compressed."
                        
                        # List files to ensure the tarball is created
                        ls -la
                        
                        # Transfer file with verbose rsync for debugging
                        echo "Transferring file..."
                        rsync -avz -e "ssh -i /var/lib/jenkins/.ssh/id_rsa" /home/temp/jenkins-file.tar.gz ubuntu@jenkins-slave:/home/temp
                        #scp -o StrictHostKeyChecking=no /home/temp/jenkins-file.tar.gz ubuntu@jenkins-slave:/home/temp
                        #scp -v -o StrictHostKeyChecking=no jenkins-file.tar.gz ubuntu@jenkins-slave:/home/temp
                        echo "File has been transferred."
                    '''
                }
            }
        }
        stage('Compressing Jenkins Files') {
            steps {
                script {
                    echo 'Compressing & backup Jenkins files to SLAVE'

                    // Check if there are files in the directory and copy them via SCP
                    sh '''
                    whoami
                    cd /
                    cd /home/temp
                    sudo tar -czvf archive-name.tar.gz /var/lib/jenkins
                    echo 'file has been compressed'
                    ls -la
                    scp -o StrictHostKeyChecking=no ./* ubuntu@jenkins-slave:/home/temp
                    echo 'file has been transfrred'
                    '''
                }
            }
        }
    }
}
