pipeline {
    agent none
    stages { 
        stage('SCM Checkout') {
            agent { label 'master' }
            steps{
            git 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git'
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