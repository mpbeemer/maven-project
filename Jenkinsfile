pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: 'localhost', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
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

        stage('Code Analysis'){
            echo 'Code Analysis needs to be moved here.'
        }
        stage('Unit Test'){
            echo 'Unit Test needs to be moved here.'
        }

        stage ('Deploy'){
            steps {
                sh "cp -f **/target/*.war /home/mpbeemer/projects/tomcat-staging/webapps"
                sh "cp -f **/target/*.war /home/mpbeemer/projects/tomcat-prod/webapps"
            }
        }
        stage('Integrations Test'){
            echo 'Integrations Test needs to be moved here.'
        }
    }
}
