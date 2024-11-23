pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/protein2005/sp-task4.git', credentialsId: 'access_for_jenkins'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat '"C:\\Program Files\\Microsoft Visual Studio\\2022\\Community\\MSBuild\\Current\\Bin\\MSBuild.exe" sokolchuk-test.sln /p:Configuration=Debug /p:Platform=x64 /m'
                    } catch (Exception e) {
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    try {
                        bat '"D:\\KPI\\SP\\lab4\\sokolchuk-test\\x64\\Debug\\sokolchuk-test.exe"'
                    } catch (Exception e) {
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
        
        failure {
            echo "Pipeline failed. Check logs to fix the issues."
        }
        
        success {
            echo "Pipeline completed successfully!"
        }
    }
}