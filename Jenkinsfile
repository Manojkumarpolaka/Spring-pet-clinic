node('mvn3.8.5') {
    stage('git') {
        git branch: 'scripted', url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git'
    }
    stage('build') {
        tool name: 'mvn3.8.5', type: 'maven'
        sh 'mvn clean package'
    }
    stage('reporting') {
           junit testResults: '**/surefire-reports/*.xml'
    }
}
