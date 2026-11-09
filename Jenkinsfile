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
                        aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 753369745113.dkr.ecr.us-east-1.amazonaws.com
                        docker build -t expense/backend:latest 753369745113.dkr.ecr.us-east-1.amazonaws.com/expense/backend:appVersion .
                        docker push 753369745113.dkr.ecr.us-east-1.amazonaws.com/expense/backend:latest
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