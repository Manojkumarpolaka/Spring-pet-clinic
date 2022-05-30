pipeline {
    agent none
    triggers {
        cron('0 * * * *')
    }
    stages { 
        stage('SCM Checkout') {
            agent { label 'master' }
            steps{
            git url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git', branch: "declarative"
            }
        }
        stage ('Artifactory configuration') {
            agent { label 'mvn3.8.5' }
            steps {
                rtMavenDeployer (
                    id: "MAVEN_DEPLOYER",
                    serverId: 'JFROG',
                    releaseRepo: 'spc-libs-release-local',
                    snapshotRepo: 'spc-libs-snapshot-local'
                )
                 withSonarQubeEnv(installationName: 'SONAR', envOnly: true, credentialsId: 'SONAR') {
                    sh "/usr/local/apache-maven-3.8.5/bin/mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar"
                 }     
            }
        }
        stage ('Exec Maven') {
            agent { label 'mvn3.8.5' }
            steps {
                withCredentials([usernamePassword(credentialsId: CREDENTIALS, usernameVariable: 'ARTIFACTORY_USERNAME', passwordVariable: 'ARTIFACTORY_PASSWORD')]) {
                    rtMavenRun (
                        tool: 'mvn3.8.5', // Tool name from Jenkins configuration
                        pom: 'pom.xml',
                        goals: 'clean install',
                        deployerId: "MAVEN_DEPLOYER"
                      
                    )
                
                }
            }
         stage('reporting') {
            agent { label 'mvn3.8.5' }
            steps {
                junit testResults: '**/surefire-reports/*.xml'
            }
        }
        }
    }
}
