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

    tools {
        SonarQubeScanner: 'sonar-8'
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


        stage('Install Dependencies'){
            steps{
                script{
                    sh """
                        npm install
                    """
                }
            }
        }

        stage('SonarQube Analysis'){
            steps{
                script{
                    withSonarQubeEnv('sonar-server') { // analysing and uploading to server
                        sh "${scannerHome}/bin/sonar-scanner"
                    }

                }
            }

        }
    }
}