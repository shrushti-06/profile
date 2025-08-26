pipeline {
    agent any

    environment {
        GH_REPO = 'https://github.com/shrushti-06/profile.git'
        GH_BRANCH = 'gh-pages'
        GITHUB_TOKEN = credentials('github-token') // Your Jenkins credential ID
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling latest code from SCM...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Static site - no build required'
            }
        }

        stage('Test') {
            steps {
                echo 'Optional: run HTML/CSS linter'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying static site to GitHub Pages'

                // Configure Git user
                sh 'git config --global user.email "jenkins@example.com"'
                sh 'git config --global user.name "Jenkins"'

                // Switch to gh-pages branch (create if needed)
                sh 'git checkout -B gh-pages'

                // Add all files
                sh 'git add .'

                // Commit changes (ignore if nothing changed)
                sh 'git commit -m "Automated deploy from Jenkins" || echo "No changes to commit"'

                // Push using GitHub token
                sh "git push -f https://${GITHUB_TOKEN}@github.com/shrushti-06/profile.git gh-pages"
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully! Site deployed to GitHub Pages.'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
