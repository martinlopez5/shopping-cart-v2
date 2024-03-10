pipeline {
    agent any

    parameters {
        booleanParam(name: 'RUN_INTEGRATION_TESTS', defaultValue: true)
    }

    stages {
        stage('Test') {
            parallel {
                stage('Unit tests') {
                    steps {
                        script {
                            sh './mvnw test -DtestGroups=unit'
                        }
                    }
                }
                stage('Integration tests') {
                    when {
                        expression {
                            return params.RUN_INTEGRATION_TESTS != 'false'
                        }
                    }
                    steps {
                        script {
                            sh './mvnw test -D testGroups=integration'
                        }
                    }
                }
            }
        }
    }
}
