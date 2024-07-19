pipeline {
    agent { node { label 'Agent-1' } }
    options {
        ansiColor('xterm')
        timeout(time: 1, unit: 'HOURS') 
    }
    environment { 
        CC = 'clang'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh '''
                    ls -ltr
                    pwd
                    echo "hello from github push webhook event"
                    printenv
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
        stage('Example') {
            environment { 
                AN_ACCESS_KEY = credentials('my-predefined-secret-text') 
            }
            steps {
                sh 'printenv'
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