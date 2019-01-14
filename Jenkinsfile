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
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv {
              sh '/usr/local/Cellar/gradle/4.10.2/libexec/bin/gradle sonar'
            }
            waitForQualityGate true
          }
        }
        stage('Test Reporting') {
          steps {
            jacoco(maximumBranchCoverage: '70')
          }
        }
      }
    }
  }
}
