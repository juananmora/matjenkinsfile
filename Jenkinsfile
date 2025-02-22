properties([
    parameters([
        string(
            name: 'REPO_URL',
            defaultValue: 'https://github.com/ctti-dev/3632.00-mat-functional-tests',
            description: 'URL where functional tests are hosted'
        ),
        choice(
            name: 'ENV_TO_TEST',
            choices: ['Desenvolupament', 'Integracio', 'Preproduccio', 'Produccio'],
            description: 'Environments to test in'
        ),
        string(
            name: 'BRANCH',
            defaultValue: 'master',
            description: 'Branch of Test Repository'
        ),
        string(
            name: 'URL_APP',
            defaultValue: 'https://qualitat.solucions.gencat.cat',
            description: 'Application URL'
        ),
        string(
            name: 'UMBRAL',
            defaultValue: '20',
            description: 'Test Failed Threshold'
        ),
        booleanParam(
            name: 'QUALITY_GATE',
            defaultValue: true,
            description: 'Enable/Disable Quality Gate'
        ),
        string(
            name: 'JIRA_PROJECT_KEY',
            defaultValue: '',
            description: 'Jira Project Key'
        ),
        string(
            name: 'JIRA_ISSUE_KEY',
            defaultValue: '',
            description: 'Jira `TEST PLAN` Issue Key'
        )
    ])
])

pipeline {
    agent any
    stages {
        stage('Trigger Remote Job') {
            steps {
                script {
                    triggerRemoteJob(
                        abortTriggeredJob: true, 
                        enhancedLogging: true, 
                        job: 'MAT-PROVES-FUNCIONAL/master/', // Nombre del job en el Jenkins remoto
                        parameters: MapParameters(parameters: [
                            MapParameter(name: 'REPO_URL', value: params.REPO_URL),
                            MapParameter(name: 'ENV_TO_TEST', value: params.ENV_TO_TEST),
                            MapParameter(name: 'BRANCH', value: params.BRANCH),
                            MapParameter(name: 'URL_APP', value: params.URL_APP),
                            MapParameter(name: 'UMBRAL', value: params.UMBRAL),
                            MapParameter(name: 'QUALITY_GATE', value: params.QUALITY_GATE.toString()), // Convertir booleano a string
                            MapParameter(name: 'JIRA_PROJECT_KEY', value: params.JIRA_PROJECT_KEY),
                            MapParameter(name: 'JIRA_ISSUE_KEY', value: params.JIRA_ISSUE_KEY)
                        ]), 
                        preventRemoteBuildQueue: true, 
                        remoteJenkinsName: 'Jenkins', // Nombre de la instalación remota en el plugin
                        useCrumbCache: true, 
                        useJobInfoCache: true
                    )
                }
            }
        }
    }
}
