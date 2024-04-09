pipeline {
    agent any

    stages {
         
        stage('Checkout') {
            
            steps {
                
                git branch: 'main',
                    url: 'https://gitlab.com/Aman42988/pipelines-java-1.git'

             }
        }

        stage ('Build') {

            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

        }

         stage ('Deploy') {
    

       steps {
           echo "deploy stage"
           deploy adapters: [tomcat9 (
                   credentialsId: 'tomcat_deployer',
                   path: '',
                   url: 'http://172.210.137.243:8081/'
               )],
               contextPath: 'test',
               onFailure: 'false',
               war: '**/*.war'
       }
   }


    }
}
