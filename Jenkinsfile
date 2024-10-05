pipeline {
    agent {
        node {
            label 'agent-1'
        }
    }
    environment { 
        packageVersion = ''

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    // build
    stages {
        stage('version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version
                    echo "application version: $packageVersion"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                sh """
                    echo  "Here I wrote shell script"
                    echo "$GREETING"
                    #sleep 10
                """
            }
        }
        
    }
    // post build
    post { 
        // always { 
        //     echo 'I will always say Hello again!'
        // }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}