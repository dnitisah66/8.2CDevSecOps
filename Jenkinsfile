pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dnitisah66/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
stage('SonarCloud Analysis') {
    environment {
        SONAR_TOKEN = credentials('SONAR_TOKEN')
    }
    steps {
        withSonarQubeEnv('SonarCloud') {
            sh '''
              ${SCANNER_HOME}/bin/sonar-scanner \
                -Dsonar.projectKey=dnitisah66_8.2CDevSecOps \
                -Dsonar.organization=dnitisah66 \
                -Dsonar.host.url=https://sonarcloud.io \
                -Dsonar.login=$SONAR_TOKEN
            '''
        }
    }
}
