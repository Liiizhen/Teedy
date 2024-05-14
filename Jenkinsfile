pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Pmd') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        stage('Generate Javadoc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/apidocs/**', fingerprint: true
        }
    }
}
