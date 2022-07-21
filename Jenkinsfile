pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true" // this should be a push
              sh "mvn clean package"
              archive 'target/*.jar' //Yes, so that they can be downloaded later
            }
        }   
    }
}
