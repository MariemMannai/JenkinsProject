pipeline {
    agent any

    stages {
         
        stage('GIT') {
            steps {
                echo 'Hello World';
                 git branch :'mariem', url: 'https://github.com/MariemMannai/DevopsProject.git'
            }
        }
        stage ('MVN CLEAN') {
            steps {
                sh 'mvn clean '
            }
        } 
 
         stage ('MVN COMPILE') {
            steps {
                sh 'mvn compile'
            }
        }

        
       
        
           
                 stage('SonarQube analysis') {
            steps {
              withSonarQubeEnv('test') {
                        sh 'mvn  sonar:sonar'
        }
                
            }
                    
                }
                 stage('testing') {
        steps{
            sh'mvn test'
        }
        post {
            always {
            junit testResults: '*/target/surefire-reports/.xml', allowEmptyResults: true
        }}
        }
          stage ('MVN NEXUS') {
            steps {
                sh  'mvn clean deploy -Dmaven.test.skip=true'
            }
        }

    
       
       
        stage('Building our image') { 

            steps { 

                script { 
                   
                   sh  'docker build -t mariemmannai/achat-back:$BUILD_NUMBER .'

                   
                }

            } 

        }
     stage('Deploy our image') { 

            steps { 

                script { 

                  	withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
        	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          sh 'docker push mariemmannai/achat-back:$BUILD_NUMBER '

                } 

            }

        } 
       
}  

        stage ('DOCKER COMPOSE') {
            steps {
                sh ' docker-compose up '
              
            }
        } 
 
         
       
    }
       
}
