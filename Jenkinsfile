pipeline {

  environment {
          AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
          AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
          datadog_apiKey = credentials('datadog_apiKey')
      }

  agent any

  stages {
    
    stage('Helm add & update Datadog repo') {
      steps {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
            sh 'helm repo add datadog https://helm.datadoghq.com'
            sh 'helm repo update'
        }
      }
    }

    stage('Helm deploy Datadog') {
      steps {
          withCredentials([file(credentialsId: 'mykubeconfig', variable: 'KUBECONFIG')]) {
            sh 'helm install datadog -f datadog-values.yaml --set datadog.site='datadoghq.com' --set datadog.apiKey='55d1154406b520e1aab9dd37e74452f5' datadog/datadog'
        }
      }
    }

  }
}