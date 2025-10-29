
 pipeline {
    agent any
    environment {
        PATH = "/usr/local/src/apache-maven/bin:$PATH"
    }
    stages {
        stage('GitHub Clone') {
            steps {
                git branch: 'Project-02', url: 'https://github.com/MagalurAdithya/Project-02.git'
            }
        }
        stage('Build Maven') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('Deploy Tomcat') {
            steps {
               deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat-id1', 
               path: '', 
               url: 'http://13.232.30.5:8080/')], 
               contextPath: 'Project-02', 
               war: '**/*.war'
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



