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
        sh 'mvn pmd:pmd'
      }
    }
    stage('K8s') {
      steps {
        sh 'kubectl set image deployments/hello-node docs=sismics/docs:latest'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: '**/target/site/**', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.jar', fingerprint: true
      archiveArtifacts artifacts: '**/target/**/*.war', fingerprint: true
    }
  }
}
