pipeline {
    agent any
    
    stages {
        stage('Code checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/viralp2020/getting-started-app.git'
            }
        }
        
        stage('image build'){
            steps{
                sh 'docker image build -t viralp1983/todoapp:v$BUILD_ID .'
                sh 'docker image tag viralp1983/todoapp:v$BUILD_ID viralp1983/todoapp:latest'
            } 
        }
        
        stage('Image Push'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    sh "docker login -u ${user} -p ${pass}"
                    sh 'docker image push viralp1983/todoapp:v$BUILD_ID'
                    sh 'docker image push viralp1983/todoapp:latest'
		    sh 'docker image rmi viralp1983/todoapp:v$BUILD_ID viralp1983/todoapp:latest'
		}
            }
        }
    }
}
