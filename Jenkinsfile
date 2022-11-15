pipeline {
agent any
stages {
stage ('Checkout') {
steps {
git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
}
}
stage('Code Quality Check via SonarQube') {
steps {
script {
def scannerHome = tool 'SonarQube';
withSonarQubeEnv('SonarQube') {
sh "${scannerHome}/bin/sonar-scanner \
  -Dsonar.projectKey=OWASP \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://192.168.245.128:9000 \
  -Dsonar.login=sqp_b5b06a1fb74ca64ddbd95aaf474fb81d30de0e14
}
}
}
}
}
post {
always {
recordIssues enabledForFailure: true, tool: sonarQube()
}
}
}
