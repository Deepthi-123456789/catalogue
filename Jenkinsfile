pipeline {
    agent {
        node {
            label 'AGENT-1'
        }
    }
    environment { 
        packageVersion = ''
    }
    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
    }
    parameters {   
        booleanParam(name: 'Deploy', defaultValue: false, description: 'Toggle this value')
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
        }
        stage('Install dependencies') {
            steps {
                sh """
                    npm install
                """
            }
        }
        stage('Unit tests') {
            steps {
                sh """
                    echo "unit tests will run here"
                """
            }
        }
        stage('Build') {
            steps {
                sh """
                    ls -la
                    #zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    #ls -ltr
                """
            }
        }
        stage('Deploy') {
            when {
                expression{
                    params.Deploy == 'true'
                }
            }
            // steps {
            //     script {
            //             def params = [
            //                 string(name: 'version', value: "$packageVersion"),
            //                 string(name: 'environment', value: "dev")
            //             ]
            //             build job: "catalogue-deploy", wait: true, parameters: params
            //         }
            // }
        }
    }
    // post build
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        failure { 
            echo 'this runs when pipeline is failed, used generally to send some alerts'
        }
        success{
            echo 'I will say Hello when pipeline is success'
        }
    }
}