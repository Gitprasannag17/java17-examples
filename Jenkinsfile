pipeline {
    agent { label 'JAVA17_MVN3.9.4' }
    triggers { 
        pollSCM('*/5 * * * *')
    }    
    stages {
        stage('scm') {
            steps {
                git 'https://github.com/Gitprasannag17/java17-examples.git'
                input message: 'Continue to the next stage?', submitter: 'devop'
            }
        }
        stage('build') {
            steps {
                sh '/usr/local/apache-maven-3.9.4/bin/mvn clean package'
            }
        }
    }
}
