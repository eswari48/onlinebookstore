pipeline {
    agent any

    tools {
        maven 'Maven3'   // Make sure this matches your Jenkins Maven installation
        jdk 'Java11'     // Optional: set this to your configured JDK name
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/eswari48/onlinebookstore.git',
                        credentialsId: 'jenki'  // Update if you use a different credential
                    ]]
                ])
                echo "Repository cloned successfully"
            }
        }

        stage('Validate') {
            steps {
                echo "Running Maven validate..."
                dir('onlinebookstore') {
                    sh 'mvn clean validate'
                }
            }
        }

        stage('Compile') {
            steps {
                echo "Compiling project..."
                dir('onlinebookstore') {
                    sh 'mvn compile'
                }
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                dir('onlinebookstore') {
                    sh 'mvn test'
                }
            }
        }

        stage('Package') {
            steps {
                echo "Packaging artifact..."
                dir('onlinebookstore') {
                    sh 'mvn package'
                    archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: false
                }
            }
        }
    }

    post {
        success {
            echo "✅ Build succeeded!"
        }
        failure {
            echo "❌ Build failed. Check console output."
        }
    }
}
