pipeline {
    agent any
    parameters {
        string(name: 'maven_version', defaultValue: '3.9.3', description: 'Pass the version of Maven')
        string(name: 'terraform_version', defaultValue: '1.8.5', description: 'Pass the version of Terraform')
        string(name: 'java_version', defaultValue: '17.0.3', description: 'Pass the version of Java') // Parameter for Java version
    }
    stages {
        stage('Download Maven') {
            steps {
                script {
                    def mavenUrl = "https://dlcdn.apache.org/maven/maven-3/${params.maven_version}/binaries/apache-maven-${params.maven_version}-bin.tar.gz"
                    sh """
                    cd /var/lib/jenkins/
                    sudo wget ${mavenUrl} -O apache-maven-${params.maven_version}-bin.tar.gz
                    sudo tar -xzf apache-maven-${params.maven_version}-bin.tar.gz
                    sudo mv apache-maven-${params.maven_version} /opt/maven
                    sudo rm apache-maven-${params.maven_version}-bin.tar.gz
                    """
                }
            }
        }
        stage('Download Terraform') {
            steps {
                script {
                    def terraformUrl = "https://releases.hashicorp.com/terraform/${params.terraform_version}/terraform_${params.terraform_version}_linux_amd64.zip"
                    sh """
                    cd /opt
                    sudo wget ${terraformUrl} -O terraform_${params.terraform_version}_linux_amd64.zip
                    sudo unzip terraform_${params.terraform_version}_linux_amd64.zip -d /usr/local/bin/
                    sudo rm terraform_${params.terraform_version}_linux_amd64.zip
                    """
                }
            }
        }
        stage('Download Java') {
            steps {
                script {
                    def javaUrl = "https://download.java.net/java/GA/jdk${params.java_version}/binaries/openjdk-${params.java_version}_linux-x64_bin.tar.gz"
                    sh """
                    cd /opt
                    sudo wget ${javaUrl} -O openjdk-${params.java_version}_linux-x64_bin.tar.gz
                    sudo tar -xzf openjdk-${params.java_version}_linux-x64_bin.tar.gz
                    sudo mv jdk-${params.java_version} /opt/java
                    sudo rm openjdk-${params.java_version}_linux-x64_bin.tar.gz
                    """
                }
            }
        }
    }
}
