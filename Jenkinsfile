pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        dotnetBuild()
      }
    }

    stage('Unit') {
      parallel {
        stage('Tests') {
          steps {
            sh 'DotNet test tests/UnitTests'
          }
        }

        stage('Integration') {
          steps {
            sh 'DotNet test tests/IntegrationTests'
          }
        }

        stage('Functional') {
          steps {
            sh 'DotNet  test tests/FunctionalTests'
          }
        }

      }
    }

    stage('Deployement') {
      steps {
        sh 'DotNet  publish eShopOnWeb.sln -o/var/aspnet'
      }
    }

  }
}