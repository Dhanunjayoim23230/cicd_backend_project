pipeline{
    agent {label 'Agent-1'}
    environment { 
        project = 'expense'
        component = 'backend'
        name = 'dhanunjaya reddy'
        DEPLOY_TO = 'QA'
        appVersion = ''
    }
    options { 
        disableConcurrentBuilds() 
        // timeout(time: 5, unit: 'SECONDS')
    }
    parameters {
       string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    } 
        stages{
            stage('Read Version'){
                steps{
                    script{
                        def packageJson = readJSON file: 'package.json'
                        appVersion = packageJson.version
                        echo "appVersion is : $appVersion"
                    }
                    
                }
            }
             stage('Dependencies install'){
                steps{
                    script{
                        sh """
                        npm install
                        """
                    }
                    
                }
            }
            stage('Docker Build'){
                steps{
                    script{
                        sh """
                        docker build -t backend:v.1.0.0
                        """
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