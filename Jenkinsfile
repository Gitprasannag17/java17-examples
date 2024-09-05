pipeline {
    agent { label 'JAVA17_MVN3.9.4' } 
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'This is maven goal' )
        choice(name: 'BRANCH_TO_BUILD', choices: ['declarative', 'master', 'scripted'], description: 'Branch to build')
    }    
    stages {
        stage('scm') {
            steps {
                git url: 'https://github.com/Gitprasannag17/java17-examples.git', branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage('build') {
            steps {
                sh "/usr/local/apache-maven-3.9.4/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
    }
   post {
        always {
            mail from: "devopsadmin@fake.com",
                to: 'team@fake.com',
                subject: "Status of the pipeline ${currentBuild.fullDisplayName}",
                body: "${env.BUILD_URL} has a result ${currentBuild.result}"

            emailext attachLog: true,
                body: """<p> Executed: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER}\'
                </b></p><p>View console outpe at "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}
                </a>"</p> <p><i>Build log is attached </i> </p>""",
                compressLog: true,
                replyTo: "do-not-reply@fake.com",
                to: "pras@fake.com",
                subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} -Status ${currentBuild.result}"


        }
    }   
}
