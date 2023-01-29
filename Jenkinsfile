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
        node(label: 'test')
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''mvn sonar:sonar \\
  -Dsonar.projectKey=Petclinic \\
  -Dsonar.host.url=http://3.7.57.95:9000 \\
  -Dsonar.login=sqp_7bf549591420e5e31fb067881827e3355f6e5e9f'''
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw "-Dtest=**/petclinic/*/*.java" test'
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

    stage('Deploy') {
      parallel {
        stage('Deploy') {
          steps {
            sh './mvnw spring-boot:run </dev/null &>/dev/null &'
          }
        }

        stage('Integration and Perfromance test') {
          steps {
            sh './mvnw verify'
          }
        }

      }
    }

  }
}