pipeline {
    agent any

    tools {
        jdk 'Java21'
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            when {
                branch 'dev'
            }
            steps {
                withSonarQubeEnv('SonarServer') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=maven-webapp'
                }
            }
        }
    }
}
