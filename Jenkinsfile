pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'dotnet build eShopOnWeb.sln'
      }
    }

    stage('Unit') {
      parallel {
        stage('Tests') {
          steps {
            sh 'test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployement') {
      steps {
        sh 'publish eShopOnWeb.sln -o/var/aspnet'
      }
    }

  }
}