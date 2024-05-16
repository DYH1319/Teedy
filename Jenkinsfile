pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('pmd') {
            steps {
                sh 'mvn -B -DskipTests pmd:pmd'
            }
        }
        stage('Doc') {
            steps {
                sh 'mvn -B -DskipTests javadoc:jar'
            }
        }
        stage('Test report') {
            steps {
                sh 'mvn -B test -Dmaven.test.failure.ignore=true'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/surefire-reports/**', fingerprint: true
        }
    }
}
