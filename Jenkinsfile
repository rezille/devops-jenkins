node {
  
  stage('Source') {
    git 'https://github.com/rezille/devops-python.git'
  }
  
  stage('SonarQube') {
    def sonarqubeScanner = tool 'SonarQube Scanner';
    withSonarQubeEnv('SonarQube Server') {
      sh "${sonarqubeScanner}/bin/sonar-scanner -Dsonar.projectKey=devops-python -Dsonar.sources=. -Dsonar.host.url=http://35.198.252.54:9000 -Dsonar.login=fb78c2252c41c3ce6863088b0cb1cd19ab737ad2"
    }
    
    timeout(time: 5, unit: 'MINUTES') {
      def qualityGate = waitForQualityGate()
      if (qualityGate.status != 'OK') {
        error "Pipeline aborted due to quality gate failure: ${qualityGate.status}"
      }
    }
    
  }
  
  stage('Deploy'){
    //TBC, transfer hello.py to hyebin:/app
  }
  
  
  
}