pipeline {
    agent any

    parameters {
        string(name: 'maven_version', defaultValue: '3.9.9', description: 'Pass the version of Maven')
        string(name: 'terraform_version', defaultValue: '1.8.5', description: 'Pass the version of Terraform')
        string(name: 'java_version', defaultValue: '17', description: 'Pass the version of Java to install')  // New parameter for Java version
    }

    stages {
        stage('Download Maven') {
            steps {
                script {
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
                    sh """
                    echo "Terraform version: ${params.terraform_version}"
                    cd /var/lib/jenkins/
                    wget https://releases.hashicorp.com/terraform/${params.terraform_version}/terraform_${params.terraform_version}_linux_amd64.zip || { echo "Terraform download failed"; exit 1; }
                    """
                }
            }
        }

        // New stage to download and install Java 17
        stage('Download Java 17') {
            steps {
                script {
                    sh """
                    echo "Java version: ${params.java_version}"
                    # Download Java 17 JDK from AdoptOpenJDK (now Adoptium)
                    cd /var/lib/jenkins/
                    wget https://github.com/adoptium/temurin17-binaries/releases/download/jdk-${params.java_version}+35/OpenJDK17U-jdk_x64_linux_hotspot_${params.java_version}+35.tar.gz || { echo "Java download failed"; exit 1; }
                    
                    # Extract the downloaded file
                    tar -xzf OpenJDK17U-jdk_x64_linux_hotspot_${params.java_version}+35.tar.gz || { echo "Java extraction failed"; exit 1; }
                    
                    # Set JAVA_HOME and update PATH (for this job)
                    export JAVA_HOME=/var/lib/jenkins/OpenJDK17U-jdk_x64_linux_hotspot_${params.java_version}+35
                    export PATH=\$JAVA_HOME/bin:\$PATH
                    echo "Java 17 installation successful."
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

