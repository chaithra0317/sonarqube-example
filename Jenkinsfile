pipeline{
    agent any
    stages{
       stage('Git Checkout Stage'){
            steps{
                git branch: 'main', url: 'https://github.com/chaithra0317/sonarqube-example.git'
            }
         }        
       stage('Build Stage'){
            steps{
                sh 'mvn clean package'
            }
         }
        stage('SonarQube Analysis Stage') {
            steps{
                withSonarQubeEnv('sonar') { 
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=demo-sonar"
                }
            }
        }
        stage('deploy'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat-server', path: '', url: 'http://13.200.246.69:8080/')], contextPath: null, war: '**/*.war'
            }
        }    
    }
}
