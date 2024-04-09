pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Install') {
            when {
                branch 'Development'
            }
            steps {
                sh 'mvn install'
            }
        }
        stage('Deploy') {
            when {
                branch 'Main'
            }
            steps {
                // Add deployment steps here (e.g., deploy war file to a server)
                echo "deploy stage"
           deploy adapters: [tomcat9 (
                   credentialsId: 'tomcat_deployer',
                   path: '',
                   url: 'http://172.210.137.243:8088/'
               )],
               contextPath: 'Demo',
               onFailure: 'false',
               war: '**/*.war'

            }
        }
    }
}
