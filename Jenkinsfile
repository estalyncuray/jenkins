pipeline {
    agent any

    tools {
        maven 'MAVEN'
    }
    stages {
        stage('Build') {
            steps {
            git url: 'https://github.com/estalyncuray/jenkins.git', branch: 'main',credentialsId:'github-credential'
                sh 'mvn clean compile'
                echo 'Application is in Build process'
            }
        }
    }
}