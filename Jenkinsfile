pipeline {
    agent any
    options { timestamps() }

    stages {
        stage('Checkout') {
            steps {
                echo 'Recuperation du code depuis GitHub'
                checkout scm
                sh 'git status'
            }
        }

        stage('Build') {
            steps {
                echo 'Verification des fichiers du projet'
                sh 'ls -la'
                sh 'test -f index.html'
                sh 'test -f style.css'
            }
        }

        stage('Test') {
            steps {
                echo 'Tests sur index.html'
                sh 'grep -q "<h1>" index.html'
                sh 'grep -q "style.css" index.html'
            }
        }

        stage('Delivery') {
            steps {
                echo 'Preparation du livrable'
                sh 'rm -rf delivery'
                sh 'mkdir delivery'
                sh 'cp index.html style.css delivery/'
                archiveArtifacts artifacts: 'delivery/**', fingerprint: true
            }
        }
    }

    post {
        success { echo 'Build OK' }
        failure { echo 'Build KO' }
    }
}
