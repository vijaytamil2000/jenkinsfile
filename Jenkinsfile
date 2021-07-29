pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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


        
        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

        // Stage 3": Upload artifiact

        stage ('Publish artificat'){
            steps {
                script {
                def NexusRepo = Version.endsWith("SNAPSHOT") ? "vijaydeveops-SNAPSHOT" : "VijayDevops-RELEASE"

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'cb81ea82-5fec-4e81-ac91-8bdea4b8b0ba', 
                groupId: "${GroupId}", 
                nexusUrl: '152.67.4.115:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
            }
            }
        }


        // Stage3 : Publish the source code to Sonarqube
        stage ('Deploy') {
            steps {
                echo 'Download artifact '
                sh 'wget --user=admin --password=Veeresh1234 http://152.67.4.115:8081/repository/vijaydeveops-SNAPSHOT/com/vijaydevopslab/vijayDevOpsLab/0.0.9-SNAPSHOT/vijayDevOpsLab-0.0.9.war'
                
                }
        }

        stage ('Download artificat') {

            steps {
                echo "deploy into tomcat folder"
                sh 'cp target/vijayDevOpsLab-0.0.9.war /usr/share/tomcat/webapps/vijayDevOpsLab-0.0.9.war'

                }
        }

        stage ('install artificat') {
            steps {
                sleep(time:5,unit:"SECONDS") 
                sh 'systemctl restart tomcat'
                }
            }

        }
}

        
        


