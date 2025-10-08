pipeline {
    agent any

    tools {
        maven 'Maven3'  // Make sure this matches the Maven installation name in Jenkins
        jdk 'Java11'    // Make sure this matches your JDK installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Cloning repository..."
                checkout scm
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
                echo "Running Maven compile..."
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                echo "Running Maven test..."
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo "Running Maven package..."
                sh 'mvn package'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo "Archiving WAR file..."
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build and artifact creation succeeded!"
        }
        failure {
            echo "❌ Build failed. Check console output!"
        }
    }
}
