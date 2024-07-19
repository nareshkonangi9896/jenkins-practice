pipeline {
    agent { node { label 'Agent-1' } }
    options {
        ansiColor('xterm')
        timeout(time: 1, unit: 'HOURS') 
    }
    // triggers { 
    //     cron('* * * * *') 
    //     }
    environment { 
        CC = 'clang'
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
        stage('credentials') {
            environment { 
                AN_ACCESS_KEY = credentials('6d12038f-7d16-4b3a-a2b5-1442de121600') 
            }
            steps {
                sh 'printenv'
            }
        }
        stage('Parameters') {
            steps {
                echo "Hello ${params.PERSON}"

                echo "Biography: ${params.BIOGRAPHY}"

                echo "Toggle: ${params.TOGGLE}"

                echo "Choice: ${params.CHOICE}"

                echo "Password: ${params.PASSWORD}"
            }
        }
        stage('Input') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "alice,bob"
                parameters {
                    string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
        }
        stage('PROD Deploy') {
        when {
            environment name: 'CC', value: 'clang'
        }
        steps {
            echo 'Deploying to PROD'
        }
        }
        stage('Parallel Stage') {
                parallel {
                    stage('Branch A') {
                        steps {
                            echo "On Branch A"
                        }
                    }
                    stage('Branch B') {
                        steps {
                            echo "On Branch B"
                        }
                    }
                    stage('Branch C') {
                        stages {
                            stage('Nested 1') {
                                steps {
                                    echo "In stage Nested 1 within Branch C"
                                }
                            }
                            stage('Nested 2') {
                                steps {
                                    echo "In stage Nested 2 within Branch C"
                                }
                            }
                        }
                    }
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