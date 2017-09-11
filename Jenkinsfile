pipeline {
  agent {
    node {
      label 'master'           
    }
  }
  tools {
        maven ' maven3.3.3'
      } 
  options {
    buildDiscarder(logRotator(numToKeepStr:'10'))
  }
  stages {

    stage('Stage') {
      
      steps {
        script {
        def javaHome = tool 'java8'
        def sonarqubeHome = tool ' sonar@10.102.22.59'
        def scannerHome = tool ''

        def sonarqubeName = ' sonar@10.102.22.59'
      }
        echo '****************************************************'
        echo 'Running Step Compile (Maven)'
        echo '****************************************************'
        script {
          if (isUnix()) {
            sh 'mvn clean compile install  -Dmaven.test.skip=true '
          } else {
            bat 'mvn clean compile install'
          }
        }
        echo '****************************************************'
        echo 'End of Step Compile (Maven)'
        echo '****************************************************'


        echo '****************************************************'
        echo 'Running Step Static Code Analysis (Sonar)'
        echo '****************************************************'
        withSonarQubeEnv($sonarqubeName) {
          bat "${scannerHome}/bin/sonar-runner.bat"
        }
        echo '****************************************************'
        echo 'End of Step Static Code Analysis (Sonar)'
        echo '****************************************************'


        echo '****************************************************'
        echo 'Running Step Unit Test (TDD)'
        echo '****************************************************'
        script {
          if (isUnix()) {
            sh 'mvn test '
          } else {
            bat 'mvn test'
          }
        }
        echo '****************************************************'
        echo 'End of Step Unit Test (TDD)'
        echo '****************************************************'


      }
    }

  }
}
