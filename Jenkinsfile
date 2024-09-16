pipeline {
    agent any
    stages {
        stage('Prepare environment') {
            steps {
                sh './gradlew compileJava'
            }
        }
        /*
        stage('Build Backend') {
            steps {
            	sleep 160
                sh './gradlew test'
            }
        }
        stage('Build') {
            steps {
            	sleep 180
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
            	sleep 100
                sh './gradlew jacocoTestReport'
                publishHTML(target: [
                    reportDir: 'build/reports/jacoco/test/html',
                    reportFiles: 'index.html',
                    reportName: 'JaCoCo Report'
                    ])
                sh './gradlew jacocoTestCoverageVerification'
            }
        }
        */
        stage('Build') {
            steps {
            	sleep 160
                sh './gradlew build'
            }
        }
        stage('Sonar') {
            steps {
                sleep 180
                sh 'docker build -t calculator .'
            }
        }
        stage('Deploy') {
            steps {
            	sleep 100
                sh 'docker push localhost:5000/calculator'
            }
        }
        /*
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
