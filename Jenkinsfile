pipeline {
  agent any
  tools {
    maven 'Maven 3.8.8'       
    jdk 'Temurin JDK 17'
  }
 
  environment {
    SONARQUBE_SERVER = 'SonarQube' 
  }
 
  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/Srinesia28/CICD', branch: 'main'
      }
    }
 
    stage('Unit Test & Coverage') {
      steps {
        sh 'mvn package'
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
        }
      }
    }
 
    stage('Static Code Analysis (SAST) via Sonar') {
      steps {
        sh """
            mvn clean compile sonar:sonar \
              -Dsonar.projectKey=springboot \
              -Dsonar.projectName='springboot' \
              -Dsonar.host.url=http://sonarqube:9000 \
              -Dsonar.token=sqp_0bf9415984ddb93a49b186019c5a60db22aca0a1
        """
      }
    }
  }
 
  post {
    success {
      echo "Pipeline berhasil 🚀"
    }
    failure {
      echo "Pipeline gagal 💥"
    }
  }
}