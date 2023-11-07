pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven 17.0.8'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Use the specified Maven tool
                    def mvnCmd = "${env.MAVEN_HOME}/bin/mvn"
                    
                    // Build the Maven project
                    sh "${mvnCmd} clean package deploy -DaltDeploymentRepository=my-repo::default::http://192.168.179.26:9081/repository/maven-releases/"
                    
                    // Deploy the artifact to Nexus
                    sh " curl -v -u admin:admin123 --upload-file /bitnami/jenkins/home/workspace/Pull_code_Nexus/target/hello-0.0.1.jar http://192.168.179.26:9081/repository/maven-releases/hello/0.0.1-SNAPSHOT/hello-0.0.1.jar"
                }
            }
        }
    }
}
