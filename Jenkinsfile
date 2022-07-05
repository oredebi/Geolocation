pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
    stages{
        stage('maven build'){
            steps{
                 sh 'mvn clean install package'
            }

        }
         stage('check pwd'){
            steps{
                sh 'pwd'
            }

        }
         stage('list directory'){
            steps{
                sh 'ls'
            }

        }
        stage('upload artifact'){
            steps{
                script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    nexusArtifactUploader artifacts:
                    [[artifactId: "${mavenPom.artifactid}",
                    classifier: '',
                    file: "target/${mavenPom.artifactid}-${mavenPom.version}.${mavenPom.packaging}",
                    type: "${mavenPom.packaging}"]],
                    credentialsId: 'Nexusid',
                    groupId: "${mavenPom.groupId}",
                       nexusUrl: '173.255.227.211:8081',
                       nexusVersion: 'nexus3',
                       protocol: 'http',
                        repository: 'biom',
                           version: "${mavenPom.version}"
                }
            }

        }
    }
}
  