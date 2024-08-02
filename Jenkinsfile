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
        }
        stage("Restore dependencies") {
            //install dependencies
        }
        stage("Build") {
            //build
        }
        stage("Run Tests") {
            //run tests
        }
    }
}