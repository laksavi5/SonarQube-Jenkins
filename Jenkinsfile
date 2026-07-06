pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarkey')
        SCANNER_HOME = tool 'sonar8.1'
    }

    stages {

        stage('Code Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/laksavi5/SonarQube-Jenkins.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarserver') {
                    bat """
                    "${SCANNER_HOME}\\bin\\sonar-scanner.bat" ^
                    -Dsonar.projectKey=demo-check ^
                    -Dsonar.projectName="SonarQube Jenkins Demo" ^
                    -Dsonar.projectVersion=1.0 ^
                    -Dsonar.sources=src/main/java ^
                    -Dsonar.login=%SONAR_TOKEN%
                    """
                }
            }
        }
    }
}
