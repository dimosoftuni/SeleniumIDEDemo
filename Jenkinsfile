pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Restore the project') {
            steps {
                bat 'dotnet restore'
            }
        }


        stage('Build the project') {
            steps {
                bat 'dotnet build'
            }
        }

        stage('Test') {
            steps {
                bat 'dotnet test --no-build --logger trx'
            }
        }

        stage('Publish Artifacts') {
            steps {
                bat 'dotnet publish SeleniumIDE/SeleniumIde.csproj -c Release -o publish'
                archiveArtifacts artifacts: 'publish/**', fingerprint: true
            }
        }
    }
    post {
        always {
            junit '**/test_results.trx'
            cleanWs()
        }
    }
}
