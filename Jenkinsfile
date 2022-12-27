pipeline {
    agent any
    tools{
        maven 'maven_3_5_0'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCreds', url: 'https://github.com/sumitkumar0296/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t sumitkumar0296/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'DockerHubCreds', variable: 'DockerHubCreds')]) {
                   sh 'docker login -u sumitkumar0296 -p ${DockerHubCreds}'

}
                   sh 'docker push sumitkumar0296/devops-integration'
                }
            }
        }
        
    }
}
