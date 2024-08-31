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
                // For a simple HTML project, this might be empty or just a placeholder
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
                    
                    // Start a simple HTTP server to serve the HTML file
                    sh 'nohup python3 -m http.server 8080 &'
                    echo 'Website is being served on http://localhost:8080'

                    // Wait for a few seconds to ensure the server starts
                    sleep(time: 5, unit: 'SECONDS')

                    // Optionally, you can curl the website to make sure it's up
                    sh 'curl -I http://localhost:8080'
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
