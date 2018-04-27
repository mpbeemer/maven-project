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
            steps {
                sh 'mvn checkstyle:checkstyle findbugs:findbugs pmd:pmd'
            }
        }
        stage('Unit Test'){
            steps {
                sh 'mvn test'
            }
        }

        stage ('Deploy'){
            steps {
                sh 'mvn package'
                sh "cp -f **/target/*.war /home/mpbeemer/projects/tomcat-staging/webapps"
                sh "cp -f **/target/*.war /home/mpbeemer/projects/tomcat-prod/webapps"
            }
        }
        stage('Integrations Test'){
            steps {
                sh 'mvn verify'
            }
        }
    }
}
