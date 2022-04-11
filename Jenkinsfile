pipeline {
    agent any
    triggers {
        cron('H */4 * * 1-5')
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
            success {
                archiveArtifacts 'target/*.jar'
            }
        }
      }
    }
}