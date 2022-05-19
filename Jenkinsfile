pipeline {
    agent none
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
                sh ''' 
                echo "PATH=${PATH}"
                echo "M2_HOME=${M2_HOME}"
                '''
                sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
            }
        }

    }
}
