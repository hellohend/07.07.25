
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
        git url: 'https://github.com/hellohend/07.07.25', branch: 'master'
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
              -Dsonar.token=sqp_807fb9bac9c968447635a414e31df2118e60f8ad
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
