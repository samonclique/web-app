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
    }
} 