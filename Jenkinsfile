pipeline {
    agent any
    
    tools {
        maven 'MAVEN'
        jdk 'JDK21'  // Must match the JDK name configured in Jenkins Tools
    }
    
    stages {
        stage('Hello') {
            steps {
                echo 'Pipeline started!'
                echo "Build number: ${env.BUILD_NUMBER}"
                echo "Building on: ${env.NODE_NAME}"
            }
        }
        
        stage('Checkout') {
            steps {
                // The checkout happens automatically when using "Pipeline script from SCM"
                echo 'Code checked out from Git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean compile'
                echo '✅ Build completed successfully!'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
                echo '✅ Tests completed successfully!'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
                echo '✅ Package completed successfully!'
            }
        }

        stage('Check Docker') {
            steps {
                sh 'docker --version'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t my-app:${env.BUILD_NUMBER} ."
                    echo '✅ Docker image built successfully!'
                }
            }
        }
    }
    
    post {
        success {
            echo '✅ Pipeline completed successfully!'
            echo "Artifact: target/*.jar"
        }
        failure {
            echo '❌ Pipeline failed! Check the logs above for errors.'
        }
        always {
            echo 'Pipeline finished.'
        }
    }
}
