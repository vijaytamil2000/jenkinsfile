pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' Testing......'

            }
        }

        // Stage 3": Upload artifiact

        stage ('Publish artificat'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'vijayDevOpsLab', classifier: '', file: 'target/vijayDevOpsLab-0.0.9.war', type: 'war']], credentialsId: 'cb81ea82-5fec-4e81-ac91-8bdea4b8b0ba', groupId: 'com.vijaydevopslab', nexusUrl: '152.67.4.115:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'vijaydeveops-SNAPSHOT', version: '0.0.9'
            }
        }


        // Stage3 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo ' Deploy'
                
                }

            }
        }

        
        
    }

