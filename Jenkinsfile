pipeline {
    agent { label 'JAVA17_MVN3.9.4' } 
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'This is maven goal' )
        choice(name: 'BRANCH_TO_BUILD', choices: ['declarative', 'master', 'scripted'], description: 'Branch to build')
    }    
    stages {
        stage('scm') {            
            steps {
                mail from: "devopsadmin@fake.com",
                to: 'pras@gmail.com',
                subject: "Cloning code for project ${env.JOB_NAME} started",
                body: "${env.BUILD_URL}"

                git url: 'https://github.com/Gitprasannag17/java17-examples.git', branch: "${params.BRANCH_TO_BUILD}"
            }
        }
        stage('build') {
            steps {
                mail from: "devopsadmin@fake.com",
                to: 'pras@fake.com',
                subject: "Build using maven for project ${env.JOB_NAME} started",
                body: "${env.BUILD_URL}"               

                sh "/usr/local/apache-maven-3.9.4/bin/mvn ${params.MAVEN_GOAL}"
            }
        }
    }
   post {
        always {
            emailext attachLog: true,
                body: """<p> Executed: Job <b>\'${env.JOB_NAME}:${env.BUILD_NUMBER}\'
                </b></p><p>View console outpe at "<a href="${env.BUILD_URL}">${env.JOB_NAME}:${env.BUILD_NUMBER}
                </a>"</p> <p><i>Build log is attached </i> </p>""",
                compressLog: true,
                replyTo: "do-not-reply@fake.com",
                to: "team@gmail.com",
                subject: "${env.JOB_NAME} - Build ${env.BUILD_NUMBER} -Status ${currentBuild.result}"
        }
    }   
}
