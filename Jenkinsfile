pipeline {
    agent none
    stages { 
        stage('SCM Checkout') {
            agent { label 'master' }
            steps{
            git branch: 'main', credentialsId: 'c1a0026b-81c4-4955-9ba0-176bc590a814', url: 'git@github.com:Manojkumarpolaka/Spring-pet-clinic.git'
            }
        }

        stage('Build package') {
            agent { label 'mvn3.8.5' }
            steps{
                sh 'mvn package'
            }
        }

        stage('Build docker image') {
            agent { label 'master' }
            steps {  
                sh 'docker build -t samplespc:$BUILD_NUMBER .'
            }
        }
    }
}