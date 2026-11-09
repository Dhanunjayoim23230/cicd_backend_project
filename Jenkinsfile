pipeline{
    agent {label 'Agent-1'}
    environment { 
        project = 'expense'
        component = 'backend'
        name = 'dhanunjaya reddy'
        DEPLOY_TO = 'QA'
    }
    options { 
        disableConcurrentBuilds() 
        // timeout(time: 5, unit: 'SECONDS')
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')

        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    } 
        stages{
            stage('build'){
                steps{
                    script{
                        sh """
                        echo "hello this is build"
                        echo " Project name is : $name"
                    
                        echo "Hello ${params.PERSON}"

                        echo "Biography: ${params.BIOGRAPHY}"

                        echo "Toggle: ${params.TOGGLE}"

                        echo "Choice: ${params.CHOICE}"

                        echo "Password: ${params.PASSWORD}"

                        """
                    }
                    
                }
            }
            stage('test'){
                steps{
                    script{
                        sh """
                        echo " hello this is test"
                        """
                    }
                    
                }
            }
            stage('deploy'){
                /* input {
                    message "Should we continue?"
                    ok "Yes, we should."
                    submitter "Dhanunjaya reddy"
                    parameters {
                        string(name: 'PERSON', defaultValue: 'Mr Dhanunjaya reddy', description: 'Who should I say hello to?')
                    }
                } */
                // when { branch 'main' }
                when { environment name: 'DEPLOY_TO', value: 'QA' 
                }
                steps{
                    script{
                        sh """
                            echo " hello this is deploy"
                            """
                    }                   
                }
            }
            stage('Parallel stages') {
                    parallel {
                        stage('STAGE-1') {
                            steps {
                                script{
                                    sh """
                                    echo "In Parallel STAGE - 1"
                                    sleep 15
                                    """
                                }                                
                            }
                        }
                        stage('STAGE-2') {
                            steps {
                                script{
                                    sh """
                                    echo "In Parallel STAGE - 2"
                                    sleep 15
                                    """
                                }                                 
                            }
                        }
                    }
                }
        }
        post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
         failure { 
            echo 'I will run when pipeline is failed!'
        }
         success { 
            echo 'I will run when pipeline is success'
        }
    }
}
