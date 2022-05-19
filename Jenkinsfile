node('master') {
    stage('git') {
        git branch: 'scripted', url: 'https://github.com/Manojkumarpolaka/Spring-pet-clinic.git'
    }
}
node('mvn3.8.5') {
    stage('build') {
        sh '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"

        '''
        sh '/usr/local/apache-maven-3.8.5/bin/mvn clean package'
    }
}
