pipeline {
    agent any
    stages {
        stage('Download Scripts') {
            steps {
            	git 'https://github.com/devops202003/python.git'
            }
        }    
        stage('List Operations') {
        	when {
        		expression { params.OPERATIONS == 'LIST' }
        	}
            steps {
                sh '''
                	sudo /usr/bin/python3 ec2-list-all.py
                '''
            }
        }
        stage('Stop Instances') {
        	when {
        		expression { params.OPERATIONS == 'STOP' }
        	}
            steps {
                sh '''
                	for i in `sudo /usr/bin/python3 ec2-list-all.py | grep Id | awk '{print $2}' | xargs`
                	do  
                		sudo /usr/bin/python3 ec2-stop-start.py off "$i"
                	done
                '''
            }
        }
        stage('Start Instances') {
        	when {
        		expression { params.OPERATIONS == 'START' }
        	}
            steps {
                sh '''
                	for i in `sudo /usr/bin/python3 ec2-list-all.py | grep Id | awk '{print $2}' | xargs`
                	do  
                		sudo /usr/bin/python3 ec2-stop-start.py on "$i"
                	done
                '''
            }
        }
    }
    post {
        success {
            echo 'SUCCESS'
        }
        failure {
            echo 'FAILED'
        }
        unstable {
            echo 'UNSTABLE'
        }
        changed {
            echo 'CHANGED'
        }
    }
}
