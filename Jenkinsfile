pipeline {
    agent any

    stages {
       stage('Date') {
          steps {
             script {
                def now = new Date()
                println now.format("yyMMdd.HHmm", TimeZone.getTimeZone('UTC'))
             }
          } 
       }
    }
 }
       

    
