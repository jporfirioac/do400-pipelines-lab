pipeline {
    agent any

    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }

    stages {
        stage('Test') {
//            parallel {
            stage('Unit Tests') {
                steps {
                    sh './mvnw test -D testGroup=unit'
                }
            }
            stage('Integration Tests') {
                when {
                    expression { return params.RUN_INTEGRATION_TESTS }
                }
                steps {
                    sh './mvnw test -D testGroups=integration'
                }
            }
//            }
        }
    }
}
