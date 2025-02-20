pipeline {
    agent any

    environment {
        DOTNET_VERSION = '8.0'
    }

    stages {

        stage('Install .NET SDK') {
            steps {
                script {
                    sh '''
                    if ! command -v dotnet &> /dev/null
                    then
                        echo ".NET SDK not found, installing..."
                        wget https://packages.microsoft.com/keys/microsoft.asc -qO- | apt-key add -
                        wget https://packages.microsoft.com/config/ubuntu/20.04/prod.list -O /etc/apt/sources.list.d/microsoft-prod.list
                        apt-get update
                        apt-get install -y dotnet-sdk-${DOTNET_VERSION}
                    else
                        echo ".NET SDK is already installed"
                    fi
                    '''
                }
            }
        }

        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
