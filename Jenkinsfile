pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn clean verify sonar:sonar \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.host.url=http://3.7.57.95:9000 \\
  -Dsonar.login=sqp_7bf549591420e5e31fb067881827e3355f6e5e9f'''
      }
    }

  }
}