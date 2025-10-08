pipeline {
    agent any

    // Set up tools installed in Jenkins
    tools {
        maven 'Maven3'   // Replace with your Maven installation name
        jdk 'Java11'     // Replace with your JDK installation name
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                git branch: 'master', url: 'https://github.com/eswari48/Hotel-Management-Project-Java.git'
                echo "Repository cloned successfully"
            }
        }

        stage('Validate') {
            steps {
                echo "Running Maven validate..."
                sh 'mvn clean validate'
            }
        }

        stage('Compile') {
            steps {
                echo "Compiling the project..."
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo "Packaging the artifact..."
                sh 'mvn package'

                // Archive the artifact in Jenkins
                archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: true
            }
        }
    }

    post {
        success {
            echo "✅ Build and artifact creation successful!"
        }
        failure {
            echo "❌ Build failed. Check console logs."
        }
    }
}
