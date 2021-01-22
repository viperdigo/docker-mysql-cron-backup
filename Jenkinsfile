
pipeline {
  environment {
    gitRepositoryUrl = "https://github.com/viperdigo/docker-mysql-cron-backup.git"
    imagenameApp = "registry.rad.app.br/docker-mysql-cron-backup"
    registryUrl = "https://registry.rad.app.br"
    registryCredential = 'registry-credentials'
    dockerImageApp = ''
    dockerImageWeb = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git([url: gitRepositoryUrl, branch: 'master', credentialsId: '8e958a5e-77b7-4857-9437-54a83625827d'])
      }
    }
    stage('Building App Image') {
      steps{
        script {
          dockerImageApp = docker.build imagenameApp
        }
      }
    }
    stage('Push Images') {
      steps{
        script {
          docker.withRegistry( registryUrl, registryCredential ) {
            dockerImageApp.push("$BUILD_NUMBER")
          }
        }
      }
    }
  }
}
