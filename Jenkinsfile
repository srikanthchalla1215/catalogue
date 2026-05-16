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
                    def scannerHome = tool name: 'sonar-8'
                    withSonarQubeEnv('sonar-server') { // analysing and uploading to server
                        sh "${scannerHome}/bin/sonar-scanner"
                    }

                }
            }

        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
        }
    }
}

        
    }
}