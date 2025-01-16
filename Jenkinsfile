pipeline {
    agent any
    environment {
        NEXUS_URL = 'http://localhost:8081/repository/maven-releases/'
        NEXUS_CREDENTIALS_ID = 'nexus'
        GIT_REPO_URL = 'git@github.com:EGamaleeva/JenkinsAndNexus.git'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: GIT_REPO_URL
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
                echo 'Maven package'
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
