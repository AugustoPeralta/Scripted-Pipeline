node {
  
  stage('Configure') {
    env.PATH = "${tool 'maven 3'}/bin:${env.PATH}"
  }
  
  stage('Checkout') {
    git 'https://github.com/AugustoPeralta/spring-boot.git'
  }

  stage('Build') {
    sh 'mvn clean package'
  }

  stage('Archive') {
    junit allowEmptyResults: true, testResults: '**/target/**/TEST*.xml'
    archive 'target/*.jar'
  }
  
  stage('SonarQube analysis') {
    withSonarQubeEnv('sonar') {
      // requires SonarQube Scanner for Maven 3.2+
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.3.0.603:sonar'
    }
  }
}
