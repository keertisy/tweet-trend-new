def registry = 'https://valaxy05.jfrog.io'
pipeline {
    agent {
        node {
            label 'maven'
        }
    }
environment {
    PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
}
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage("build"){
            steps {
                 echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                 echo "----------- build complted ----------"
            }
        }
        stage("test"){
            steps{
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                 echo "----------- unit test Complted ----------"
            }
        }

    stage('SonarQube analysis') {
    environment {
      JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64/bin/java'
      scannerHome = tool 'sonarqube-scanner'
    }
    steps{
    withSonarQubeEnv('sonarqube-scanner') {  
      sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }
  stage("Quality Gate"){
    steps {
        script {
        timeout(time: 1, unit: 'HOURS') {  
    def qg = waitForQualityGate()  
    if (qg.status != 'OK') {
      error "Pipeline aborted due to quality gate failure: ${qg.status}"
    }
  }
}
    }
  } 
}
}