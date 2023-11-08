pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool 'Maven 17.0.8'
        NEXUS_USER = 'admin'
        NEXUS_PASSWORD = 'admin123'
        NEXUS_IP = '192.168.179.26'
        NEXUS_PORT = '9081'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    // Use the specified Maven tool
                    def mvnCmd = "${env.MAVEN_HOME}/bin/mvn"
                    
                    // Build the Maven project
                    sh "${mvnCmd} clean package"
                    
                    // Deploy the artifact to Nexus
                    // sh " curl -v -u admin:admin123 --upload-file /bitnami/jenkins/home/workspace/Pull_code_Nexus/target/hello-0.0.1.jar http://192.168.179.26:9081/repository/maven-releases/hello/0.0.1-SNAPSHOT/hello-0.0.1.jar"
                }
            }
        }

        stage('Upload Artifact'){
            steps{
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '${NEXUS_IP}:${NEXUS_PORT}',
                    groupId: 'zufarexplainedit',
                    version: 0.0.1,
                    repository: 'maven-releases',
                    credentialsId: '${NEXUS_LOGIN}',
                    artifacts: [
                        [artifactId: hello,
                         classifier: '',
                         file: 'hello-0.0.1.jar',
                         type: 'jar']
                    ]
                ) 
            }
            
        }
    }
}
