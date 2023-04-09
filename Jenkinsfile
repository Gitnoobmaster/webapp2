pipeline {
    agent any

tools{
maven 'maven_3.9.1'


}

    stages {
        stage('GitHub Sourcesss') {
            steps {
                echo 'Brining code from Git'
                    git branch: 'release/devl', credentialsId: '7690fd09-25d3-4d30-bfd3-27fa31e5560b', url: 'git@github.com:Gitnoobmaster/webapp.git'
            }
        }
        stage('Maven Build') {
            steps {
                echo 'Building code now'
                sh  "mvn clean package" } 
                }
        stage('Test - Sonar') {
            steps {
                echo 'Testing phase'
                sh "mvn sonar:sonar" }
            }
        stage('Move artiface to nexus repo') {
             steps {
                echo 'Moving build artifact'
                sh "mvn deploy" } 
        }
        stage('Deploying to Tomcat Server') {
            steps {
                echo 'Coying the artifact to Tomcat webapps folder'
                sshagent(['24463778-9aa4-4cfd-b3f2-1f7a25293148']) {
                sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.233.164.125:/opt/apache-tomcat-10.1.7/webapps/" } }
            }
        }

}