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
                    echo installing .NET SDK 6.0
                    choco install dotnet -sdk -y --version-6.0.100
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