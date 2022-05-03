pipeline {
    agent none
    stages { 
        stage('SCM Checkout') {
            agent { label 'master' }
            steps{
            git url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git', branch: "main"
            }
        }

        stage('Build package') {
            agent { label 'maven_docker' }
            steps{
                sh 'sudo mvn clean package'
            }
        }

        stage('Build docker image') {
            agent { label 'maven_docker' }
            steps {  
                sh 'sudo docker build -t samplespc:$BUILD_NUMBER .'
            }
        }
    }
}
