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

        stage('Build package') {
            agent { label 'mvn3.8.5' }
            steps{
                withSonarQubeEnv(installationName: 'SONAR', envOnly: true, credentialsId: 'SONAR') {
                    sh "/usr/local/apache-maven-3.8.5/bin/mvn clean package sonar:sonar"
                }
            }
        }
    }
}
