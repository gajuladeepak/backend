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
        stage('Test') { 
            steps {
                sh 'echo this is build'
            }
        }
        stage('Deploy') { 
            when {
                //branch 'production'
                expression { env.GIT_BRANCH == "origin/main" }
            }
            steps {
                sh 'echo this is build'
                ////error 'pipeline failed'
            }
        }
       

    post {
        always{
            echo "This sections runs always"
            deleteDir()
        }
    }


}

}


