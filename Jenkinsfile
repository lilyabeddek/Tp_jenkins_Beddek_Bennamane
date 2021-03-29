pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'C:\\Users\\Rcom\\Desktop\\gradle-5.6\\bin\\gradle build'
        bat 'C:\\Users\\Rcom\\Desktop\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

  }
}