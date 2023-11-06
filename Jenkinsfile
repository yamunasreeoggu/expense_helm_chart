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
          git branch: 'main', url: "https://github.com/yamunasreeoggu/${COMPONENT}"
        }
        sh 'helm upgrade -i ${COMPONENT} . -f APP/helm/${ENV}.yaml --set appVersion=${VERSION}'
      }
    }
  }

  post {
    always {
    cleanWs()
    }
  }

}

