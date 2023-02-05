pipeline {
  agent {
    node {
      label 'test'
    }

  }
  stages {
    stage('Compile') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.host.url=http://172.31.27.134:9000 \\
  -Dsonar.login=sqp_1c3cc19ff8242b79e117bb7c6fb6347b6f33ec42'''
      }
    }

    stage('Unit Test/Archive JUnit-formatted test result') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
        junit '**/target/surefire-reports'
      }
    }

  }
}