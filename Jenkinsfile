pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-access-token', url: 'https://github.com/Reshmasthan/maven-web-application-2.git']])
                
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
                sh 'pwd && ls -lrt && cd target && ls -lrt'
            }
        }
        stage('Nexus Artifact Upload') {
            steps {
                script {
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'maven-web-application', 
                            classifier: '', 
                            file: "target/maven-web-application-1.0.0-SNAPSHOT.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus-access', 
                    groupId: 'com.mt', 
                    nexusUrl: '43.204.147.221:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'nexus-artifact-repository', 
                    version: '1.0.0-SNAPSHOT'
                }
            }
        }
    }
}
