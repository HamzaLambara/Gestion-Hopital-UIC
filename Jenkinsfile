pipeline {
    agent any
    stages {
        stage('Prepare environment') {
            steps {
                sh './gradlew compileJava'
            }
        }
        stage('Build Backend') {
            steps {
                sh './gradlew test'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew jacocoTestReport'
                publishHTML(target: [
                    reportDir: 'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                    ])
                sh './gradlew jacocoTestCoverageVerification'
            }
        }
        stage('Sonar') {
            steps {
                sh './gradlew jacocoTestReport'
                publishHTML(target: [
                    reportDir: 'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                    ])
                sh './gradlew jacocoTestCoverageVerification'
            }
        }
        stage('Deploy') {
            steps {
                sh './gradlew build'
            }
        }
        /*
        stage('Push Backend Docker Image') {
            steps {
                sh 'docker build -t calculator .'
            }
        }
        stage('Build Frontend') {
            steps {
                sh 'docker push localhost:5000/calculator'
            }
        }
        stage('Deploy Frontend') {
            steps {
                sh 'docker rm calculator'
                sh 'docker run -d -p 8765:8080 --name calculator localhost:5000/calculator'
            }
        }
        stage("Acceptance Tests") {
            steps {
                sleep 60
                sh './gradlew acceptanceTest -Dcalculator.url=http://localhost:8765'
            }
        }
        */
    }
    post {
        always {
            sh 'docker stop calculator'
        }
    }
}
