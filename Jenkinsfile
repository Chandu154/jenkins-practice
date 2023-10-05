pipeline {

    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
    } 
    // triggers {
    //    cron('* * * * *')
    //}
    // it is global environment and accesable to all environments
    environment { 
        USER = 'chandu'
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

        stage('Perms') {
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
        stage('PROD deploy'){
            when{
                branch 'master'
            }
            steps{
                echo "deploying to PROD"
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
