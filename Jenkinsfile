pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Clone github repo') {
            steps {
                git branch: 'main', url: 'https://github.com/keertisy/tweet-trend-new/'  
            }
        }
    }
}
