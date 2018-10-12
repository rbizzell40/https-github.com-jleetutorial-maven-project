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
                sh 'mvn clean package'
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
                        sh "scp **/target/*.war ec2-user@${paras.tomcat_dev}:/var/lib/tomcat8/webapps -i /Jenkins.pem"
                    }
                }

            }
        }
    }
}