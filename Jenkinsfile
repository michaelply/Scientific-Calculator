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
                junit '**/target/surefire-reports/TEST-*.xml'
            }
            success {
                archiveArtifacts 'target/*.jar'
            }
        }
      }
    }
}