pipeline {

    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    } 
    // it is global environment and accesable to all environments
    environment { 
        USER = 'chandu'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building ..'
                  sh '''
                    ls -ltr
                    pwd
                    echo "Hello from github push webhook event"
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
        // below one is particular satge environment
        stage('Example') {
            environment { 
                AUTH = credentials('ssh-auth') 
            }
            steps {
                sh 'printenv'
            }
        }
    }
    
        post { 
        always { 
            echo 'I will always say Hello again!'
        }
        success{
            echo 'I will run only when job is success'
        }
        failure{
            echo 'I will run when failure'
        }
    }
}
