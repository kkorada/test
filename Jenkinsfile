pipeline {
  agent {
    def javaHome = tool 'java8'
      def sonarqubeHome = tool 'sonarqube@59'
      def scannerHome = tool 'sonar-scanner2.8'

      def sonarqubeName = 'sonarqube@59'
    node { lable 'master'
      tools {
        maven 'maven3'
      }
    }
  }
        
  stages {

    stage('Commit Stage') {
      steps {
      
        echo '****************************************************'
        echo 'Running Step Compile (Maven)'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn clean compile install  -Dmaven.test.skip=true '
        else
          bat 'mvn clean compile install'
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
        if (isUnix())
          sh 'mvn test '
        else
          bat 'mvn test'
        echo '****************************************************'
        echo 'End of Step Unit Test (TDD)'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Maven Job'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn deploy  -Dmaven.test.skip=true '
        else
          bat 'mvn deploy'
        echo '****************************************************'
        echo 'End of Step Maven Job'
        echo '****************************************************'

      
      }
    }
    
    stage('ACCEPTANCE STAGE - FUNCTIONAL TEST') {
      steps {
      
        echo '****************************************************'
        echo 'Running Step Shell Job'
        echo '****************************************************'
        if (isUnix())
          sh 'cf push'
        else
          bat 'cf push'
        echo '****************************************************'
        echo 'End of Step Shell Job'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Maven Job'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn test '
        else
          bat 'mvn test'
        echo '****************************************************'
        echo 'End of Step Maven Job'
        echo '****************************************************'

      
      }
    }
    
    stage('ACCEPTANCE STAGE -  AUTOMATED SYSTEM INTEGRATION') {
      steps {
      
        echo '****************************************************'
        echo 'Running Step Shell Job'
        echo '****************************************************'
        if (isUnix())
          sh 'cf push'
        else
          bat 'cf push'
        echo '****************************************************'
        echo 'End of Step Shell Job'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Shell Job'
        echo '****************************************************'
        if (isUnix())
          sh 'cf push'
        else
          bat 'cf push'
        echo '****************************************************'
        echo 'End of Step Shell Job'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Maven Job'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn test '
        else
          bat 'mvn test'
        echo '****************************************************'
        echo 'End of Step Maven Job'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Packaging Production Artifact (Nexus)'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn clean release:clean release:prepare release:perform  -Dmaven.test.skip=true '
        else
          bat 'mvn clean release:clean release:prepare release:perform'
        echo '****************************************************'
        echo 'End of Step Packaging Production Artifact (Nexus)'
        echo '****************************************************'

      
      }
    }
    
    stage('ACCEPTANCE STAGE - LOAD + PERFORMANCE TEST') {
      steps {
      
        echo '****************************************************'
        echo 'Running Step ADC-Environment Provision (CF)'
        echo '****************************************************'
        if (isUnix())
          sh 'cf push'
        else
          bat 'cf push'
        echo '****************************************************'
        echo 'End of Step ADC-Environment Provision (CF)'
        echo '****************************************************'

      
        echo '****************************************************'
        echo 'Running Step Maven Job'
        echo '****************************************************'
        if (isUnix())
          sh 'mvn gatling:exec '
        else
          bat 'mvn gatling:exec'
        echo '****************************************************'
        echo 'End of Step Maven Job'
        echo '****************************************************'

      
      }
    }
    
    stage('PRODUCTION STAGE') {
      steps {
      
        echo '****************************************************'
        echo 'Running Step Shell Job'
        echo '****************************************************'
        if (isUnix())
          sh 'cf push'
        else
          bat 'cf push'
        echo '****************************************************'
        echo 'End of Step Shell Job'
        echo '****************************************************'

      
      }
    }
    
  }
}
