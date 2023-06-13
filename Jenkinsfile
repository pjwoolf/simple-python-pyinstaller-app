node {
    stage('Build') {
        checkout scm
        docker.image('python:2-alpine') {
            sh 'python -m py_compile sources/add2vals.py sources/calc.py'
        }
    } 
    stage('Test') {
        try {
            checkout scm
            docker.image('qnib/pytest') {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            } 
        } catch (e) {
            throw e
        } finally {
            junit 'target/surefire-reports/results.xml'
        }
    }
}