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
  }
}