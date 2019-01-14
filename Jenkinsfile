pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        failure {
          mail(subject: 'failure', body: 'The build failed', from: 'jenkins@jenkins.com', to: 'mossabinfo@gmail.com')

        }

        success {
          mail(subject: 'Success', body: 'The build successeded', from: 'jenkins@jenkins.com', to: 'mossabinfo@gmail.com')

        }

      }
      steps {
        sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle build'
        sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle javadoc'
        sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle jar'
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Success', body: 'The build was successful', from: 'jenkins@jenkins.com', to: 'mossabinfo@gmail.com')
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Test Reporting') {
          steps {
            jacoco(maximumBranchCoverage: '70')
          }
        }
        stage('Code Analysis') {
          steps {
            sh '/Users/mac/sonar-scanner/bin/sonar-scanner'
            waitForQualityGate true
          }
        }
      }
    }
    stage('Deployment') {
      when {
        branch 'master'
      }
      steps {
        sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle uploadArchives'
      }
    }
    stage('Slack Notification') {
      when {
        branch 'master'
      }
      steps {
        slackSend(message: 'Hello this is jenkins')
      }
    }
  }
}