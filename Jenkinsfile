pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/StevenSawant/cicd.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                // Add any necessary build steps for your project
            }
        }
        stage('Test') {
            steps {
                script {
                    echo 'Testing...'
                    // Check if the HTML file exists
                    def htmlFile = 'index.html'
                    if (fileExists(htmlFile)) {
                        echo "HTML file exists: ${htmlFile}"
                    } else {
                        error "HTML file does not exist!"
                    }

                    // Simple validation: Check if the HTML file contains a <title> tag
                    def content = readFile(htmlFile)
                    if (content.contains("<title>")) {
                        echo "HTML file contains a <title> tag."
                    } else {
                        error "HTML file does not contain a <title> tag!"
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying...'

                    // Use the full path to the Python executable if necessary
                    // On Windows, it might be something like: 'C:\\Python39\\python.exe'
                    bat 'C:\Users\truea\AppData\Local\Programs\Python\Python312 hello.py' 
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