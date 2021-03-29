pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'D:\\gradle-5.6\\bin\\gradle build'
        bat 'D:\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

  }
}