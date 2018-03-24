
pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat_dev', defaultValue: 'localhost:8090', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost:9090', description: 'Production Server')
    } 
 
    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }
 
stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
 
        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "cp **/target/*.war 'C:/Program Files/apache-tomcat-8.5.28/webapps'"
                               
                    }
                }
 
                stage ("Deploy to Production"){
                    steps {
                     bat "cp **/target/*.war 'C:/Program Files/apache-tomcat-8.5.28-preproduction/webapps'"
                    }
                }
            }
        }
    }
}
