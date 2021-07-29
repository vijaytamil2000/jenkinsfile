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
                nexusArtifactUploader artifacts: [[artifactId: 'vijayDevOpsLab', classifier: '', file: 'target/vijayDevOpsLab-0.0.9-SNAPSHOT.war', type: 'war']], credentialsId: 'cb81ea82-5fec-4e81-ac91-8bdea4b8b0ba', groupId: 'com.vijaydevopslab', nexusUrl: '152.67.4.115:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'vijaydeveops-SNAPSHOT', version: '0.0.9-SNAPSHOT'
            }
        }


        // Stage3 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo 'Download artifact '
                sh 'wget --user=admin --password=Veeresh0987# http://152.67.4.115:8081/repository/vijaydeveops-SNAPSHOT/com/vijaydevopslab/vijayDevOpsLab/0.0.9-SNAPSHOT/vijayDevOpsLab-0.0.9-*-4.war'
                
                }

            steps {
                echo "deploy into tomcat folder"
                sh 'cp target/vijayDevOpsLab-0.0.9-*-4.war /usr/share/tomcat/webapps/vijayDevOpsLab-0.0.9-*-4.war'

            }

            steps {
                sleep(time:5,unit:"SECONDS") 
                sh 'systemctl restart tomcat'
                }
            }

            }
}

        
        


