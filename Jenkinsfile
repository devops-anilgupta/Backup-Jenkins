pipeline{
    agent any

    stages{
        stage('Jenkins Backup')
        {
            echo "1. Staring the jenkins backup"   
            // steps{
            //     sh '''
            //         cd /var/lib
            //         zip -r jenkins-backup.zip jenkins
            //     '''
            // }
        }
        stage('Upload to Jenkins compressed file to another server')
        {
            steps{
                echo "2. Upload to Jenkins compressed file to another server" 
                sh '''
                    cd /
                    scp ./testing-scp-copy.txt root@jenkins-slave:/home && rm ./testing-scp-copt.txt
                '''
            }
        }
    }
}