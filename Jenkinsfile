pipeline {
    agent any
    
    tools {
      maven "mvn3.8.4"
    }

    stages {
      stage('Build stage') {
        steps {
            sh 'echo ${Test method}'
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
           sh 'mvn test -DDockerTest#${Test method}'
       }
    }


    stage('Clean Workspace') {
      steps {
        cleanWs()
      }
    }
  }
}
