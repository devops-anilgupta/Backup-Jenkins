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
                    whoami
                    cd /
                    cd /home/temp/
                    rsync -avz -e "ssh -i /var/lib/jenkins/.ssh/id_rsa" /home/temp/jenkins-file.tar.gz ubuntu@jenkins-slave:/home/temp
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
