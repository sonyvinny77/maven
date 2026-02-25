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

        stage('Quality Gate') {
            when {
                branch 'dev'
            }
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }

    }
}
