pipeline {
    agent any

    stages{
        stage("Checout code") {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/wondertedy7/JenkinsSeleniumIde_demo_01.08'
            }
        }
        stage("Setup .Net Core") {
            //install dotnet
            steps {
                bat '''
                echo Downloading .NET SDK 6.0
                curl -l -o dotnet-sdk-6.0.424-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/9e184641-56bb-430b-9297-4316b039b641/3409ae071e0140ce2237f909b4b0ffbb/dotnet-sdk-6.0.424-win-x86.exe
                echo Installing .NET SDK 6.0
                dotnet-sdk-6.0.424-win-x86.exe /quiet /norestart
                '''   
            }

        }
        stage("Restore nuget packages") {
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }

        }
        stage("Build") {
            //build
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration release'
            }
        }
        stage("Run Tests") {
            //run tests
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"' // след като се изпълнят тестовете, логъра ще запише резултатите в ProgramData/Jenkins/jenkins/workspace
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            smstest testResultsFile: '**/TestResults/*.trx'
        }
    }
}