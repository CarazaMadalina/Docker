pipeline {
    agent any
    
    tools {
      maven "mvn3.8.4"
    }

    stages {
      stage('Build stage') {
        steps {
            sh 'echo ${TestMethod}'
            sh 'mvn clean install -DskipTests'
        }
      }

      stage('Test stage') {
        when {
           expression { BRANCH == "master" }
        }
       agent {
        label 'built-in'
       }

       steps {
           sh 'mvn test -Dtest="DockerTest#${TestMethod}"'
       }
    }


    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
  }
}
