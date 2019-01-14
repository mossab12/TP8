pipeline {
  agent any
  stages {
    stage('Build') {
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
    stage('Test Reporting') {
      steps {
        jacoco(maximumBranchCoverage: '70')
      }
    }
    stage('Deployment') {
      steps {
        sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle uploadArchives'
      }
    }
    stage('Slack Notification') {
      steps {
        slackSend(baseUrl: 'https://matrix-enh1669.slack.com', channel: 'matrix', message: 'Hello this is jenkins', teamDomain: 'matrix-enh1669', token: 'https://hooks.slack.com/services/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', tokenCredentialId: 'UEJNE2MN3')
      }
    }
  }
}