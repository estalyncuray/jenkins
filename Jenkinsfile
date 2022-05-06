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
            }
        }
        stage('Test') {
            steps {
                echo 'mvn -Dmaven.test.skip=true'
            }
        }
        stage('SonarQube') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn verify sonar:sonar \
                       -Dsonar.host.url=http://malic-devops.duckdns.org:9000 \
                       -Dsonar.projectKey=musker \
                       -Dsonar.projectName=Musker'
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time:5, unit:'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy process'
            }
        }
    }
}