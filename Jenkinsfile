pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarkey') // Jenkins secret text credential ID
    }

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Venkiemc/sonarqube-jenkins-project.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarserver') { // 'sonarserver' is the name you configured
                    bat """
                        "C:\\Program Files\\sonar-scanner\\bin\\sonar-scanner.bat" ^
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
