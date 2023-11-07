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
                    sh "${mvnCmd} clean package"
                    
                    // Deploy the artifact to Nexus
                    sh "${mvnCmd} deploy:deploy-file " +
                       "-Durl=http://192.168.179.26:9081/repository/maven-rereases/ " +
                       "-DrepositoryId=nexus-releases " +
                       "-Dfile=target/hello-0.0.1.jar " +
                       "-DgroupId=zufarexplainedit " +
                       "-DartifactId=hello " +
                       "-Dversion=0.0.1 " +
                       "-Dpackaging=jar"
                }
            }
        }
    }
}
