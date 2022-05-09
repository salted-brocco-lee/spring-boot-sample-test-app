pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build Start Running'
        bat 'mvn -B -DskipTests clean package'
        echo 'Build Done'
        archiveArtifacts '**/target/*.jar'
      }
    }

    stage('Unit') {
      parallel {
        stage('Unit') {
          steps {
            echo 'Unit Start Running'
            bat 'mvn -Dtest="com.example.testingweb.smoke.**" test'
            echo 'Unit Done'
          }
        }

        stage('Integration') {
          steps {
            echo 'Integration Start Running'
            bat 'mvn -Dtest="com.example.testingweb.integration.**" test'
            echo 'Integration Done'
          }
        }

        stage('Functionnal') {
          steps {
            echo 'Functionnal Start Running'
            bat 'mvn -Dtest="com.example.testingweb.functional.**" test'
            echo 'Functionnal Done'
          }
        }

      }
    }

    stage('Deploy') {
      when {
        expression {
          currentBuild.result == null || currentBuild.result == 'SUCCESS'
        }
      }
      steps {
        input(message: 'Voulez-vous Deployer ?', ok: 'Allons-y')
        echo 'Deploy Start'
        bat 'mvn -B -DskipTests install'
        echo 'Deploy Done'
      }
    }
    post {
      success{
        mail to 'benoit.hert@gmail.com'
      }
    }
  }
  tools {
    maven 'maven3.8.5'
    jdk 'jdk'
  }
}