pipeline {
    agent any

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
                            // Esta condición verifica el valor de la variable booleana
                            return params.RUN_INTEGRATION_TESTS != 'false'
                        }
                    }
                    steps {
                        script {
                            sh './mvnw test -DtestGroups=integration'
                        }
                    }
                }
            }
        }
    }

    parameters {
        booleanParam(name: 'RUN_INTEGRATION_TESTS', defaultValue: true, description: 'Determina si se deben ejecutar las pruebas de integración')
    }
}
