node {
  stage('build & deploy') {
    openshiftBuild bldCfg: 'get-started-node',
      namespace: 'development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'get-started-node',
      namespace: 'development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'get-started-node',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'get-started-node',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'get-started-node',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'get-started-node',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'get-started-node',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'get-started-node',
      namespace: 'production'
  }
}