
  stage('build & deploy') {
    openshiftBuild bldCfg: 'getstartednode',
      namespace: 'development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'getstartednode',
      namespace: 'development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'getstartednode',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'getstartednode',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'getstartednode',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'getstartednode',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'getstartednode',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'getstartednode',
      namespace: 'production'
  }
}