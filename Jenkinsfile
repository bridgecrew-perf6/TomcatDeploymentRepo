pipeline {
    agent any

    tools {
        // Install the Maven version configured as "maven" and add it to the path.
        maven "maven"
    }

    stages {
        stage('SCM - Checkout') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'stable', url: 'https://github.com/arafath478/TomcatDeploymentRepo.git'

            }
        
         }
        
       stage('Build') {
            steps {
//                  To run Maven on a windows agent, command use for windows batch
//                    bat "mvn -Dmaven.test.failure.ignore=true clean package"
                
//                  To run Maven on a linux agent, command use for shell
                      sh 'mvn clean package'
            }
        }
       stage('Deploy') {
//          deploy to container plugin
//                steps {
//                deploy adapters: [tomcat8(credentialsId: 'TomcatAdminUser', path: '', url: 'http://35.89.152.212:8090/')], contextPath: 'TomcatApplicationPipeline', war: '**/*.war'
//                }
//           deploy to tomcat using scp command
               steps {
                sshagent(['TomcatServerCredientials']) {
                   sh "scp -o StrictHostKeyChecking=no target/TomcatDeploy.war ec2-user@34.211.229.93:/opt/apache-tomcat-8.5.79/webapps"
                 }
               }
        
         }
         
      
     }
    post{
        always{
         echo "Job finished"
        }
        success{
         echo "Build success by yasar arafath"
        }
        failure{
         echo "Build failed by yasar arafath"
        }  
    }
}
