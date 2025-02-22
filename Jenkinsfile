properties([
    parameters([
        string(
            name: 'REPO_URL',
            defaultValue: 'https://github.com/ctti-dev/3632.00-mat-performance-tests',
            description: 'URL del repositorio de código fuente'
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
            name: 'PROTOCOL',
            defaultValue: 'https',
            description: 'Protocol of Application URL: https o http'
        ),
        string(
            name: 'URL_APP',
            defaultValue: 'qualitat.solucions.gencat.cat',
            description: 'Application URL to test without protocol'
        ),
        string(
            name: 'TEST_DURATION',
            defaultValue: '10',
            description: 'Test Duration'
        ),
        string(
            name: 'RAMP_UP_TIME',
            defaultValue: '60',
            description: 'Ramp Up Time'
        ),
        string(
            name: 'THREAD_COUNT',
            defaultValue: '20',
            description: 'Thread Count'
        ),
        booleanParam(
            name: 'QUALITY_GATE',
            defaultValue: true,
            description: 'Enable/Disable Quality Gate'
        ),
        string(
            name: 'UMBRAL',
            defaultValue: '20',
            description: 'Test Failed Threshold'
        ),
        string(
            name: 'JIRA_PROJECT_KEY',
            defaultValue: 'DEVSECOPS2',
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
        stage('Trigger Remote Performance Test') {
            steps {
                script {
                    triggerRemoteJob(
                        abortTriggeredJob: true,
                        enhancedLogging: true,
                        job: 'MAT-PROVES-RENDIMENT/master/', // Name of the job in the remote Jenkins
                        parameters: [
                            string(name: 'REPO_URL', value: params.REPO_URL),
                            string(name: 'ENV_TO_TEST', value: params.ENV_TO_TEST),
                            string(name: 'BRANCH', value: params.BRANCH),
                            string(name: 'PROTOCOL', value: params.PROTOCOL),
                            string(name: 'URL_APP', value: params.URL_APP),
                            string(name: 'TEST_DURATION', value: params.TEST_DURATION),
                            string(name: 'RAMP_UP_TIME', value: params.RAMP_UP_TIME),
                            string(name: 'THREAD_COUNT', value: params.THREAD_COUNT),
                            booleanParam(name: 'QUALITY_GATE', value: params.QUALITY_GATE),
                            string(name: 'UMBRAL', value: params.UMBRAL),
                            string(name: 'JIRA_PROJECT_KEY', value: params.JIRA_PROJECT_KEY),
                            string(name: 'JIRA_ISSUE_KEY', value: params.JIRA_ISSUE_KEY)
                        ],
                        preventRemoteBuildQueue: true,
                        remoteJenkinsName: 'Jenkins', // Name of the remote Jenkins installation in the plugin
                        useCrumbCache: true,
                        useJobInfoCache: true
                    )
                }
            }
        }
    }
}
