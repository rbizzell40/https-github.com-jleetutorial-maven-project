pipeline {
    agent any
    tools {
        rtMaven.tool = "Maven-3.6.0"
        maven 'localMaven'
    }
    stages{

        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
