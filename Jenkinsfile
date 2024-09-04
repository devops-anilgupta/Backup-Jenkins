pipeline{
    agent{
        label 'Built-In'
    }
    stages{
        stage('Jenkins Backup')
        {
            steps{
                sh '''
                    cd /var/lib
                    zip -r jenkins-backup.zip jenkins
                '''
            }
        }
        stage('Upload to Jenkins compressed file to another server')
        {
            steps{
                sh '''
                    scp ./testing-scp-copy.txt root@jenkins-slave:/home && rm ./testing-scp-copt.txt
                '''
            }
        }
    }
}