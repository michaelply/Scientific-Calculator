pipeline {
    agent any
    triggers {
        cron('H/5 * * * *')
    }
    stages {
      stage("clean") {
        agent any
        steps {
            withSonarQubeEnv('mysonar') {
                sh 'mvn clean'
            }
        }
      }
      stage("build") {
        agent any
        steps {
            withSonarQubeEnv('mysonar') {
                sh 'mvn package'
            }
        }
      }
      stage("test") {
        agent any
        steps {
            withSonarQubeEnv('mysonar') {
                sh 'mvn test'
            }
        }
      }
      stage("static analysis") {
        agent any
        steps {
            withSonarQubeEnv('mysonar') {
                sh 'mvn clean package sonar:sonar'
            }
        }
      }
        post {
            always {
                junit testResults: '**/target/surefire-reports/TEST-*.xml', skipPublishingChecks: true, allowEmptyResults: true
            }
            success {
                archiveArtifacts 'target/*.jar'
            }
        }
      }
    }
}