pipeline {
    agent {
        label 'Agent-1'
    }
    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
        //retry(1)
    }

    environment {
        DEBUG = 'true'
        appVersion = '' //this will become global, we can use across pipelines
    }

    stages {
        stage('Read the version') { 
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') { 
            steps {
                sh 'npm install'
            }
        }
        stage('Deploy build') { 

            steps {
                sh """

                docker build -t deepakgajula/backend:${appVersion}
                """
            }
        }

    }

       

    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
    }


}


