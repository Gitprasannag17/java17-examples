node('JAVA17_MVN3.9.4') {
    stage('git') {
        git 'https://github.com/Gitprasannag17/java17-examples.git'
    }
    stage('build') {
        sh '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"
        '''
        sh '/usr/local/apache-maven-3.9.4/bin/mvn clean package'
    }
    stage('archive') {
        archiveArtifacts artifacts: 'target/*.jar', followSymlinks: false
    }
    stage('publish test reports') {
        junit '**/TEST-*.xml'
    }
}