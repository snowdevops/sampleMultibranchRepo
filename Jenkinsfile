pipeline {
   agent any
   tools {
      maven 'Maven'
   }
   stages {
       stage("build") {
           steps {
              snDevOpsStep()
               echo "Building" 
                sh 'mvn clean install -DskipTests'
               //sleep 5
           }
       }
       
     stage("test") {
           stages {
            stage('UAT unit test1') {
                steps {
                        snDevOpsStep ()
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                       
            }
            stage('UAT unit test 2') {
                 steps {
                         snDevOpsStep ()
                        echo "Testing"
                        sh 'mvn -Dtest=com.sndevops.eng.App1Test test'                     
                }
            }     
        }
      
      }
           
      stage("test-1") {
                steps {
                        snDevOpsStep ()
                        echo "Testing"
                       // sh 'mvn -Dtest=com.sndevops.eng.AppTest test'
                }                    
        }

       stage("deploy") {
         stages{
             stage('deploy UAT') {
                when{
                   branch 'dev'
                }
               steps{
                 snDevOpsStep ()
                 echo "deploy in UAT"
               }
             }
            stage('deploy PROD') {
               when {
                  branch 'master'
               }
                steps{
                  snDevOpsStep ()
                   echo "deploy in prod"
                  snDevOpsChange()              
                }
            }
        }
      }
     
    }
    post {
              always {
              junit '**/target/surefire-reports/*.xml' 
              }
        }
     
  }
