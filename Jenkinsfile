node('mvn3.8.5') {
    stage('git') {
        git branch: 'scripted', url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git'
    }
    stage('build') {
        sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
    }
    stage('reporting') {
        steps {
           junit testResults: '**/surefire-reports/*.xml'
        }
    }
}
