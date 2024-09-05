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
                    cd /
                    if [ -f ./testing-scp-copy.txt ]; then
                        scp -o StrictHostKeyChecking=no ./testing-scp-copy.txt root@jenkins-slave:/home || { echo "SCP failed"; exit 1; }
                    else
                        echo "File does not exist"
                        exit 1
                    fi
                    '''
                }
            }
        }
    }
}
