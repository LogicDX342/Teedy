pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Docs') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }
        stage('pmd'){
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        stage('Test report') {
            steps {
                bat 'mvn test --fail-never'
                bat 'mvn surefire-report:report'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true
        }
    }
}