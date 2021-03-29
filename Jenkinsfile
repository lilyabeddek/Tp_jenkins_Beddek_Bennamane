pipeline {
  agent any
  stages {
    stage('Build') {
      post {
        failure {
          mail(subject: "ERROR BUILD: Projet -> ${env.JOB_NAME}",body: "<br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", to: 'hl_beddek@esi.dz')
        }

      }
      steps {
        bat 'D:\\grdle-5.6\\bin\\gradle build'
        bat 'D:\\gradle-5.6\\bin\\gradle javadoc'
        archiveArtifacts 'build/libs/*.jar, build/docs/javadoc/*'
        archiveArtifacts 'build/test-results/test/*'
      }
    }

    stage('Mail notification') {
      steps {
        mail(subject: "New push [github]: Projet -> ${env.JOB_NAME}", body: "Un push a été fait avec success <br>Project: ${env.JOB_NAME} <br>Build Number: ${env.BUILD_NUMBER} <br> URL de build: ${env.BUILD_URL}", to: 'hl_beddek@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat(script: 'D:\\gradle-5.6\\bin\\gradle sonarqube', returnStatus: true)
            }

            waitForQualityGate true
          }
        }

        stage('Test reporting') {
          steps {
            cucumber 'reports/*.json'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        bat 'D:\\gradle-5.6\\bin\\gradle publish'
      }
    }

    stage('Slack notification') {
      steps {
        slackSend(baseUrl: 'https://hooks.slack.com/services/', channel: 'tp-jenkins', token: 'T01NG7VH880/B01S6APL8T1/SOREG7NXa4Ys3w3vcxBxXOBd', teamDomain: 'Esi', message: 'a new push has been added', color: '#008000')
      }
    }

  }
}
