pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                    ls -ltr
                    pwd
                    echo "hello from github push webhook event"
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                //error 'this is failed'
            }
        }
    }
    post { 
        always { 
            echo 'I will always run whether the job is success or not'
        }
        success { 
            echo 'I will run only when job is success'
        }
        failure { 
            echo 'I will run when failure'
        }
    }
}