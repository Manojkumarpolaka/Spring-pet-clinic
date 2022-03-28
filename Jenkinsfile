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
                sh ''' 
                echo "PATH=${PATH}"
                echo "M2_HOME=${M2_HOME}"
                '''
                sh '/usr/local/apache-maven-3.8.4/bin/mvn clean package'
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