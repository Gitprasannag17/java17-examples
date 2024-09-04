pipeline {
    agent { label 'JAVA17_MVN3.9.4' }
    triggers { upstream(upstreamProjects: 'starter-project', threshold: hudson.model.Result.SUCCESS) }
    stages {
        stage('scm') {
            steps {
                git 'https://github.com/Gitprasannag17/java17-examples.git'
            }
        }
        stage('build') {
            steps {
                sh '/usr/local/apache-maven-3.9.4/bin/mvn clean package'
            }
        }
    }
}
