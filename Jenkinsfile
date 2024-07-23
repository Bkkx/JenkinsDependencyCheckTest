pipeline {
    agent any
    environment {
        NVD_API_KEY = credentials('nvd-api-key') // Use the ID you set in the credentials
    }
    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/Bkkx/JenkinsDependencyCheckTest.git'
            }
        }
        stage('OWASP DependencyCheck') {
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML --nvdApiKey ${NVD_API_KEY} --suppression suppression.xml', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}