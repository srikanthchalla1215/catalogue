pipeline{
    agent {
        node {
            label 'ROBOSHOP'
        }
    }
     
     environment{
        appVersion = ''
     }

    options {
        disableConcurrentBuilds()
    }

    stages{
        stage('Read version'){
            steps{
                script{
                    def packageJson = readJSON file: 'package.json'
        
            // Access the 'version' property directly
                    def appVersion = packageJson.version
        
                     echo "Current Version: ${appVersion}"
                }
            }

        }
    }
}