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
            deploy adapters: [tomcat9(credentialsId: 'war-deployer', path: '', url: 'http://13.200.246.69:8080/')], contextPath: null, war: '**/*.war'
           }
     }    
    }
}
