pipeline {
    agent any
    stages {
        stage('Download Operations') {
            steps {
                git url: https://github.com/devops202003/python.git
            }
        }
        stage('Stop Instances') {
            when {
                expression { params.OPERATION == 'STOP' }
            }
            steps {
                sh '
                    cd ${env.WORKSPACE}/python
                    for i in `/bin/python3 ec2-list-all.py  | grep Id:| awk '{print $NF}' | xargs`
                    do
                        /bin/python3 ec2-stop-start.py OFF "$i"
                    done
                '
            }
        }
        stage('Start Instances') {
            steps {
                sh 'echo "Start Instances"'
            }
        }
    }
    post {
        success {
            echo 'Stack has been created'
        }
        failure {
            echo 'Stack Creation Failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
