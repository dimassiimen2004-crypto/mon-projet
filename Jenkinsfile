pipeline {
    agent any
    options { timestamps() }

    stages {
        stage('Checkout') {
            steps {
                echo 'Recuperation du code depuis GitHub'
                checkout scm
                bat 'git status'
            }
        }

        stage('Build') {
            steps {
                echo 'Verification des fichiers du projet'
                bat 'dir'
                bat 'if not exist index.html exit /b 1'
                bat 'if not exist style.css exit /b 1'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests sur index.html'
                bat 'findstr /C:"<h1>" index.html >nul'
                bat 'findstr /C:"style.css" index.html >nul'
            }
        }

        stage('Delivery') {
            steps {
                echo 'Preparation du livrable'
                bat 'if exist delivery rmdir /s /q delivery'
                bat 'mkdir delivery'
                bat 'copy index.html delivery\\ /Y'
                bat 'copy style.css delivery\\ /Y'
                archiveArtifacts artifacts: 'delivery/**', fingerprint: true
            }
        }
    }

    post {
        success { echo 'Build OK' }
        failure { echo 'Build KO' }
    }
}
