pipeline {
    agent any
    triggers {
        cron('H/5 * * * *')
    }
    stages {
      stage("build & SonarQube analysis") {
        agent any
        steps {
            withSonarQubeEnv('mysonar') {
                sh 'mvn clean package sonar:sonar'
            }
        }
        post {
            always {
                junit testResults: '**/target/surefire-reports/TEST-*.xml', skipPublishingChecks: true
            }
            success {
                archiveArtifacts 'target/*.jar'
            }
        }
      }
    }
}