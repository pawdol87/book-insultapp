try {
    timeout(time: 20, unit: 'MINUTES') {
        node('maven') {
            stage('mvn clean package') {
                checkout scm
                sh 'mvn clean package'
            }

            stage('build') {
                openshiftBuild(buildConfig: 'test', showBuildLogs: 'true')
            }

            stage('deploy') {
                openshiftDeploy(deploymentConfig: 'test')
            }
        }
    }

} catch (err) {
    echo "in catch block"
    echo "Caught: ${err}"
    currentBuild.result = 'FAILURE'
    throw err
}