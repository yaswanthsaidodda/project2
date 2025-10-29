
 pipeline {
    agent any
    environment {
        PATH = "/usr/local/src/apache-maven/bin:$PATH"
    }
    stages {
        stage('GitHub Clone') {
            steps {
                git branch: 'project2', url: 'https://github.com/yaswanthsaidodda/project2.git'
            }
        }
        stage('Build Maven') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('Deploy Tomcat') {
            steps {
              deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://13.234.59.44:8080/')], contextPath: 'project2', war: '**/*.war'
            }
        }
    }
    post {
        success {
            emailext to: "adithyamagalur@gmail.com",
            recipientProviders: [developers()],
            subject: "jenkins Pipe : ${currentBuild.currentResult}: ${env.JOB_NAME}",
            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\n More Info can be found here: ${env.BUILD_URL}",

            attachLog: true
            
            slackSend message: "Build deployed successfully - Job ${env.JOB_NAME}\n More Info can be found here: ${env.BUILD_URL}"
 
        }
    }
}



