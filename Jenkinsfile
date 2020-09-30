node {
  stage('Construir y Desplegar') {
    openshiftBuild bldCfg: 'hellopythonapp',
      namespace: 'development05',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'development05'
  }
  stage('Aprobar (Pruebas)') {
    input message: 'Aprobado para Pruebas?',
      id: 'approval'
  }
  stage('Desplegar en Pruebas') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'development05',
      srcTag: 'latest',
      destinationNamespace: 'testing05',
      destStream: 'hellopythonapp',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'testing05'
  }
  stage('Aprobar (Produccion)') {
    input message: 'Aprobado para Produccion?',
      id: 'approval'
  }
  stage('Desplegar en Produccion') {
    openshiftTag srcStream: 'hellopythonapp',
      namespace: 'development05',
      srcTag: 'latest',
      destinationNamespace: 'production05',
      destStream: 'hellopythonapp',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'hellopythonapp',
      namespace: 'production05'
  }
}
