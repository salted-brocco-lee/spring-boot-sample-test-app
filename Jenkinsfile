pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Start Running'
        bat 'mvn -B -DskipTests clean package'
        echo 'Build Done'
      }
    }

  }
  tools {
    maven 'maven3.8.5'
    jdk 'jdk'
  }
}