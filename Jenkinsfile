pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Choose Environment')
    choice(name: 'COMPONENT', choices: ['frontend', 'backend'], description: 'Choose Component')
    string(name: 'VERSION', defaultValue: '', description: 'Version to Deploy')
  }

  stages {

    stage('Deployment') {
      steps {
        dir('APP') {
          git branch: 'main', url: "https://github.com/yamunasreeoggu/${COMPONENT}" # frontend has many files due to which helm cannot handle pods creation, hence we are using below dir(HELM) step to change the dir to run the pipeline
        }
        dir('HELM') {
          git branch: 'main', url: "https://github.com/yamunasreeoggu/expense_helm_chart"
          sh 'helm upgrade -i ${COMPONENT} . -f ${WORKSPACE}/APP/helm/${ENV}.yaml --set appVersion=${VERSION}'
        }
      }
    }
  }

  post {
    always {
    cleanWs()
    }
  }

}

