pipeline {
    agent any

    stages {
       stage('Date') {
          steps {
             script {
                def now = new Date()
                println now.format("yyyy-MM-dd.HHmm", TimeZone.getTimeZone('UTC'))
             }
          } 
       }
    }
 }
       

    
