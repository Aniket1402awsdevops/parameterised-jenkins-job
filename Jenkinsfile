pipeline {
    agent any

    tools {
        // Automatically install tools that are configured in Jenkins
        maven 'Maven 3.9.3'   // Make sure Maven is installed in Jenkins
        jdk 'JDK 11'          // Ensure JDK 11 is configured in Jenkins (or the appropriate version)
        terraform 'Terraform 1.5.0' // Ensure Terraform is configured in Jenkins
    }

    environment {
        // Any environment variables can be defined here
        MAVEN_HOME = tool name: 'Maven 3.9.3', type: 'ToolLocation'
        JAVA_HOME = tool name: 'JDK 11', type: 'ToolLocation'
        TERRAFORM_HOME = tool name: 'Terraform 1.5.0', type: 'ToolLocation'
    }

    parameters {
        string(name: 'BRANCH', defaultValue: 'main', description: 'Branch to checkout')
        string(name: 'ENVIRONMENT', defaultValue: 'dev', description: 'Target Environment (dev, staging, prod)')
    }

    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    // Checkout the code from the Git repository
                    checkout scm
                }
            }
        }

        stage('Download Dependencies') {
            steps {
                script {
                    // Ensure the necessary tools are installed and available
                    echo "Using Maven: ${MAVEN_HOME}"
                    echo "Using Java: ${JAVA_HOME}"
                    echo "Using Terraform: ${TERRAFORM_HOME}"
                }
            }
        }

        stage('Build Project') {
            steps {
                script {
                    // Run Maven to build the project (for example)
                    sh "${MAVEN_HOME}/bin/mvn clean install -DskipTests"
                }
            }
        }

        stage('Terraform Init') {
            steps {
                script {
                    // Run Terraform commands, if applicable
                    sh "${TERRAFORM_HOME}/bin/terraform init"
                    sh "${TERRAFORM_HOME}/bin/terraform apply -auto-approve"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Example deployment stage (you can modify it as needed)
                    echo "Deploying to ${params.ENVIRONMENT} environment"
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }

        failure {
            echo "Pipeline failed!"
        }

        always {
            cleanWs()  // Clean up the workspace after the job is done
        }
    }
}
