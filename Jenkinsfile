pipeline {
    agent any

    parameters {
        string(name: 'maven_version', defaultValue: '3.9.9', description: 'Pass the version of Maven')
        string(name: 'terraform_version', defaultValue: '1.8.5', description: 'Pass the version of Terraform')
    }

    stages {
        stage('Download Maven') {
            steps {
                script {
                    // Check if the version passed is valid, and adjust URL accordingly
                    sh """
                    echo "Maven version: ${params.maven_version}"
                    cd /var/lib/jenkins/
                    wget https://dlcdn.apache.org/maven/maven-3/${params.maven_version}/binaries/apache-maven-${params.maven_version}-bin.tar.gz || { echo "Maven download failed"; exit 1; }
                    """
                }
            }
        }

        stage('Download Terraform') {
            steps {
                script {
                    // Check if the version passed is valid, and adjust URL accordingly
                    sh """
                    echo "Terraform version: ${params.terraform_version}"
                    cd /opt
                    wget https://releases.hashicorp.com/terraform/${params.terraform_version}/terraform_${params.terraform_version}_linux_amd64.zip || { echo "Terraform download failed"; exit 1; }
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Download successful!'
        }
        failure {
            echo 'Download failed.'
        }
    }
}
