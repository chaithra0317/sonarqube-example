pipeline{
    agent {label 'sonar'}
    tools {
        maven 'maven'
    }    
    stages{
       stage('Git Checkout Stage'){
            steps{
                git branch: 'main', url: 'https://github.com/chaithra0317/sonarqube-example.git'
            }
         }        
       stage('Build Stage'){
            steps{
                sh 'mvn clean install'
            }
      }       
      stage('SonarQube Analysis Stage') {
            steps{
                withSonarQubeEnv('sonar') { 
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=sonar-jenkins"
                }
            }
     }
     stage('deploy'){
            steps{
               sh 'sudo cp /home/ubuntu/workspace/sonar-demo/target/*.war /home/ec2-user/apache-tomcat-9.0.82/webapps'
'
            }
        }    
    }
}
