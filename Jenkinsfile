pipeline {
    agent any

    parameters {
        string(name: 'maven_version', defaultValue: '3.9.3', description: 'Pass the version of Maven')
        string(name: 'terraform_version', defaultValue: '1.8.5', description: 'Pass the version of Terraform')
    }

    stages {
        stage('Download Maven') {
            steps {
                script {
                    // Ensure parameters are passed correctly and variables are interpolated in shell
                    sh """
                    cd /var/lib/jenkins/
                    sudo wget https://dlcdn.apache.org/maven/maven-3/${params.maven_version}/binaries/apache-maven-${params.maven_version}-bin.tar.gz || { echo "Maven download failed"; exit 1; }
                    """
                }
            }
        }

        stage('Download Terraform') {
            steps {
                script {
                    // Ensure parameters are passed correctly and variables are interpolated in shell
                    sh """
                    cd /opt
                    sudo wget https://releases.hashicorp.com/terraform/${params.terraform_version}/terraform_${params.terraform_version}_linux_amd64.zip || { echo "Terraform download failed"; exit 1; }
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
