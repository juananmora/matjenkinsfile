properties([
    parameters([
        string(
            name: 'REPO_URL',
            defaultValue: 'https://github.com/ctti-dev/3632.00-mat-api-tests',
            description: 'URL del repositorio de pruebas de API'
        ),
        choice(
            name: 'ENV_TO_TEST',
            choices: ['Desenvolupament', 'Integracio', 'Preproduccio', 'Produccio'],
            description: 'Entorno en el que se ejecutarán las pruebas'
        ),
        string(
            name: 'BRANCH',
            defaultValue: 'master',
            description: 'Rama del repositorio de pruebas'
        ),
        string(
            name: 'APP_NAME',
            defaultValue: 'conference',
            description: 'URL base de la API a probar'
        ),
        string(
            name: 'JIRA_PROJECT_KEY',
            defaultValue: 'DEVSECOPS2',
            description: 'Clave del proyecto Jira'
        ),
        string(
            name: 'JIRA_ISSUE_KEY',
            defaultValue: '',
            description: 'Clave de la incidencia Jira `TEST PLAN`'
        )
    ])
])

pipeline {
    agent any
    stages {
        stage('Trigger Remote API Test') {
            steps {
                script {
                    triggerRemoteJob(
                        abortTriggeredJob: true,
                        enhancedLogging: true,
                        job: 'MAT-PROVES-API/master/', // Nombre del job en el Jenkins remoto
                        parameters: [
                            string(name: 'REPO_URL', value: params.REPO_URL),
                            string(name: 'ENV_TO_TEST', value: params.ENV_TO_TEST),
                            string(name: 'BRANCH', value: params.BRANCH),
                            string(name: 'APP_NAME', value: params.APP_NAME),
                            string(name: 'JIRA_PROJECT_KEY', value: params.JIRA_PROJECT_KEY),
                            string(name: 'JIRA_ISSUE_KEY', value: params.JIRA_ISSUE_KEY)
                        ],
                        preventRemoteBuildQueue: true,
                        remoteJenkinsName: 'Jenkins-API', // Nombre de la instalación remota de Jenkins en el plugin
                        useCrumbCache: true,
                        useJobInfoCache: true
                    )
                }
            }
        }
    }
}
