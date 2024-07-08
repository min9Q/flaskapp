pipeline {
   agent any
   parameters {
      choice(name: 'VERSION', choices: ['1.1.0','1.2.0','1.3.0'], description: '')
      booleanParam(name: 'executeTests', defaultValue: true, description: '')
   }
   stages {
      stage("Build") {
         steps {
               sh 'docker build -t flask-jenkins:v1.1.0 .'
         }
      }
      stage("Tag and Push") {
         steps {
              sh "docker tag jenkins-pipeline_web:v1.1.0 ${DOCKER_USER_ID}/jenkins-app:${BUILD_NUMBER}"
               sh "docker login -u ${DOCKER_USER_ID}-p ${DOCKER_USER_PASSWORD}"
               sh "docker push ${DOCKER_USER_ID}/jenkins-app:${BUILD_NUMBER}"
         }
      }
      stage("deploy") {
         steps {
               echo 'deploying the applicaiton...'
         }
      }
   }
}
