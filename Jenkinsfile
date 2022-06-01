node('mvn3.8.5') {
    tool name: 'mvn3.8.5', type: 'maven'
    stage('git') {
        git branch: 'scripted', url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git'
    }
    stage('build') {
        sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
    }
    stage('reporting') {
           junit testResults: '**/surefire-reports/*.xml'
    }
}
