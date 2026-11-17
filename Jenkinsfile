pipeline {
    agent any
    options {
        skipDefaultCheckout()
    }
    parameters {
        string(name: 'THREADS', defaultValue: '2', description: '가상 사용자 수 (5 이하)')
        string(name: 'LOOPS', defaultValue: '5', description: '반복 횟수 (10 이하)')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Smoke Test') {
            steps {
                bat '%JMETER_HOME%\\bin\\jmeter.bat -n -f -t perf/smoke.jmx -l reports/smoke.jtl -e -o html-report -Jthreads=%THREADS% -Jloops=%LOOPS%'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'reports/, html-report/', allowEmptyArchive: true
        }
    }
}
