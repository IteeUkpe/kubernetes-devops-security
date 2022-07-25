

pipeline {
  agent any

  stages {

    /*stage('Build Artifact - Maven') {
      steps {
        //sh "mvn clean package -DskipTests=true"
        //archive 'target/*.jar'
      }
    }

    stage('Unit Tests - JUnit and JaCoCo') {
      steps {
        //sh "mvn test"
      }
      /*post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }*/

    /*stage('Nginx App Protect - Docker') {
      steps {
        parallel(
          "Nginx App Protect Requirements": {
            sh "ansible-galaxy install -r requirements.yml --force"
          },
          "Deploy_NAP": {
            sh "ansible-playbook -i hosts app-protect.yml"
          },
          "Workaround_DNS": {
            sh 'ansible-playbook -i hosts copy-nginx-conf.yml'
          }
        )
      }
    }
    */

    /*stage('Docker Build and Push') {
      steps {
        withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
          sh 'printenv'
          sh 'docker build -t iteeukpe/numeric-app:""$GIT_COMMIT"" .'
          sh 'docker push iteeukpe/numeric-app:""$GIT_COMMIT""'
        }
          sh 'docker run -d -p 3000:3000 bkimminich/juice-shop'
      }
    }
    */

    
    stage ('Execute Ansible') {
      steps{
            sh "ansible-playbook ../tasks/main.yml"
          }
        }
     
    
    
    stage('Kubernetes Deployment - DEV') {
      steps {
        withKubeConfig([credentialsId: 'kubeconfig']) {
          /*sh "sed -i 's#replace#iteeukpe/numeric-app:${GIT_COMMIT}#g' k8s_deployment_service.yaml"*/
          sh "kubectl apply -f k8s_deployment_service.yaml"
        }
      }
    }

    stage('OWASP ZAP - DAST') {
      steps {
        withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'bash zap.sh'
        }
      }
    }
    
  }

}