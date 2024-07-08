pipeline {
   agent any
   environment {
      NEW_VERSION = '1.0.0'
      ADMIN_CREDENTIALS = credentials('admin_user_credentials')
   }
   stages {
      stage("build") {
         when {
            expression {
               env.GIT_BRANCH == 'origin/master'
            }
         }
         steps {
            echo 'building the applicaiton...'
            echo "building version ${NEW_VERSION}"
         }
      }
      stage("test") {
         when {
            expression {
               env.GIT_BRANCH == 'origin/test' || env.GIT_BRANCH == ''
            }
         }
         steps {
            echo 'testing the applicaiton...'
         }
      }
      stage("deploy") {
         steps {
            echo 'deploying the applicaiton...'
            withCredentials([[$class: 'UsernamePasswordMultiBinding',
               credentialsId: 'admin_user_credentials',
               usernameVariable: 'admin_user',
               passwordVariable: '1234'
            ]]) {
               sh 'printf ${USER}'
            }
         }
      } 
   }
   post {

         always {

            echo 'building..'

         }

         success {

               echo 'success'

         }

         failure {

               echo 'failure'

         }

      }

   }
