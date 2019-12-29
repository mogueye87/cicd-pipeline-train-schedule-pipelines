pipeline {
    agent any
    stages {
        stage('Build'){
         steps {
            echo 'Running build automation'
            sh './gradlew build --no-daemon'
            archiveArtifacts artifacts: 'dist/trainSchedule.zip'
         }
      }
       stage('Upload to AWS') {
             steps {
                 withAWS(region:'eu-west-3',credentials:'webserver_login') {
                 sh 'echo "Uploading content with AWS creds"'
                     s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'dist/trainSchedule.zip', bucket:'project3-jenkins-pipeline-on-aws')
                 }
             }
        }
    }
}
