pipeline {
    agent any
    environment {
        NEXUS_URL = 'http://localhost:8081/repository/maven-releases/'
        NEXUS_CREDENTIALS_ID = 'nexus'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'git@github.com:EGamaleeva/JenkinsAndNexus.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Upload to Nexus') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: NEXUS_URL,
                    groupId: 'com.example',
                    version: '1.0.0',
                    repository: 'maven-releases',
                    credentialsId: NEXUS_CREDENTIALS_ID,
                    artifacts: [
                        [artifactId: 'my-app', classifier: '', file: 'target/my-app-1.0.0.jar', type: 'jar']
                    ]
                )
            }
        }
    }
    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
