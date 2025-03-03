pipeline {
    agent any

    tools {
        maven 'Maven 3.x'  // Ensure Maven is configured in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/bnaik1982/DevopsProjectSampleJavaApp.git'  // Replace with your repository
            }
        }

        stage('Build & Run PMD') {
            steps {
                sh 'mvn clean verify'  // Runs PMD check
            }
        }

        stage('Publish PMD Report') {
            steps {
                recordIssues(
                    tool: pmdParser(),
                    pattern: '**/target/pmd.xml'
                )
            }
        }
    }
}
