pipeline {
    agent any
    environment {
        DOTNET_VERSION = '8.0'
    }
    stages {
        stage('Checkout source code') {
            steps {
                checkout scm
            }
        }
        stage('Setup .NET SDK') {
            steps {
                sh 'dotnet --version || echo "Installing .NET SDK..."'
                // Jenkins агенти обикновено вече имат SDK инсталиран.
                // Ако не – добави предварителна конфигурация със собствени образи или shell скрипт.
            }
        }
        stage('Restore dependencies') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet restore'
                    } else {
                        bat 'dotnet restore'
                    }
                }
            }
        }
        stage('Build application') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet build --no-restore'
                    } else {
                        bat 'dotnet build --no-restore'
                    }
                }
            }
        }
        stage('Run Tests') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'dotnet test --no-build --verbosity normal'
                    } else {
                        bat 'dotnet test --no-build --verbosity normal'
                    }
                }
            }
        }
    }
}
