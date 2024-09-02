pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/StevenSawant/cicd.git', branch: 'main'
            }
        }
        stage('Run Python Script') {
            steps {
                script {
                    echo 'Running Python Script...'

                    // Use the full path to the Python executable if necessary
                    // On Windows, it might be something like: 'C:\\Python39\\python.exe'
                    bat 'python hello.py'
                }
            }
        }
    }
    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
