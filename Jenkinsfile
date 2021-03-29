pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'D:\\ESI\\Tresor Esi\\Tresor Sup esi\\Trésor 2CS\\Tresors peronnel\\OGL\\gradle-5.6\\bin\\gradle build'
        bat 'D:\\ESI\\Tresor Esi\\Tresor Sup esi\\Trésor 2CS\\Tresors peronnel\\OGL\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/docs/javadoc/*'
      }
    }

  }
}