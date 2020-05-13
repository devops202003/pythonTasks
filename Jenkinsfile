pipeline {
    agent any
    stages {
        stage('Stop Instances') {
            steps {
                sh 'echo "Stop Instances"'
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
