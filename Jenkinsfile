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
        stage('Build & code analysis') {
            agent { label 'mvn3.8.5' }
            steps{
                withSonarQubeEnv(installationName: 'SONAR', envOnly: true, credentialsId: 'SONAR') {
                    sh "/usr/local/apache-maven-3.8.5/bin/mvn clean package org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.1.2184:sonar"
                }
            }
        }
        stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
           }
        }
    }
}
