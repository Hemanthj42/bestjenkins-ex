pipeline {
    agent any
    
    environment{
         PATH = "/opt/maven-3.3.9/bin:$PATH"
         
    }
    stages {
        
        stage('build') {
            steps {
                sh "mvn clean package"
            }
        }
        
        stage('sonar') { 
             steps {
                 withSonarQubeEnv('sonar1') {
                     sh "mvn sonar:sonar"
                     }
                }
            
        stage('upload artifacts') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'projectking', classifier: '', file: 'target/java-tomcat-maven-example.war', type: 'WAR']], credentialsId: 'nxs', groupId: 'hjking', nexusUrl: '13.233.62.50:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'hjpipeline', version: '11.0-SNAPSHOT'
            }
        }   
        
        }          
    }
}
   
