pipeline {
    agent any

    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }

    stages {
//        stage('Test') {
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
        stage('Build') {
            steps {
                script {
                    try {
                        sh './mvnw package -D skipTests'
                    }
                    catch (ex) {
                        echo "Error while generating JAR file"
                        throw ex
                    }
                }
            }
        }

//            }
//        }
    }
}
