pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                // Checkout code from GitHub and specify the branch
                git branch: 'main', url: 'https://github.com/Desi-Kamenova/SelenuimWebDriver_Jenkins'
            }
        }

        stage('Set up .Net Core') {
            steps {
                bat '''
                echo Downloading .Net 6 Sdk
                curl -l -o dotnet-sdk-6.0.132-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/ad59f1d1-5f19-4474-86be-2f09ab195618/5c7a64445dae84e386bb88e1f6ac09e4/dotnet-sdk-6.0.132-win-x86.exe
                echo installing dotnet-sdk-6.0.132-win-x86.exe
                dotnet-sdk-6.0.132-win-x86.exe /quiet /norestart
                '''
            }
        }

        stage('Restoring nuget packages') {
            steps {
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }

        stage('Build') {
            steps {
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }

        stage('Run TestProject1 tests') {
            steps {
                bat '''
                echo "Running TestProject1 tests"
                dotnet test TestProject1/TestProject1.csproj --verbosity normal
                '''
            }
        }

        stage('Run TestProject2 tests') {
            steps {
                bat '''
                echo "Running TestProject2 tests"
                dotnet test TestProject2/TestProject2.csproj --verbosity normal
                '''
            }
        }

        stage('Run TestProject3 tests') {
            steps {
                bat '''
                echo "Running TestProject3 tests"
                dotnet test TestProject3/TestProject3.csproj --verbosity normal
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            junit '**/TestResults/*.trx'
        }
    }
}