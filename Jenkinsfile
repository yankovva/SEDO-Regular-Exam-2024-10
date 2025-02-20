pipeline {
    agent any

    stages {

        stage('Restore Dependencies') {
            steps {
                echo 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                echo 'dotnet build --no-restore'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
