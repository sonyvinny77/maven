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
                echo "Running SonarQube scan for dev branch"
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'prod'
            }
            steps {
                echo "Deploying to production..."
            }
        }
    }
}
