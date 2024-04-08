pipeline{
    agent any
    tools {
        maven "maven3"
    }
    stages {
        stage("Git clone") {
            steps {
            git branch: 'main', url: 'https://github.com/samonclique/web-app.git'
            }
        }
        stage('Build') {
            steps {
                sh '''
                mvn clean
                mvn test
                mvn package
                '''
            }
        }
        stage('Sonarqube Analysis') {
            environment {
                    scannerhome = tool 'sonar5'
                }
            steps {
                script  {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonar-key') {
                        sh "${scannerhome}/bin/sonar-scanner -Dsonar.projectKey=web-app -Dsonar.projectName=sam-web-app"
                    }
                }
            }
        }
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
                }
            }
        }
    }
} 