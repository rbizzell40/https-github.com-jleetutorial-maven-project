pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '18.221.239.117', description: 'Staging Server')
    }

    triggers {
         pollSCM('* * * * *')
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
                        bat "copy -i C:\\Users\\Karthik Kodur Mohan\\Desktop\\private key\\Jenkins.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat8/webapps"
                    }
                }

            }
        }
    }
}