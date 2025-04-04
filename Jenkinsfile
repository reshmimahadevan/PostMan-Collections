pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        stage('Checkout') {
            steps {
                git url: 'https://github.com/reshmimahadevan/PostMan-Collections'
            }
        }

        stage('Pull Docker Image') {
            steps {
                bat 'docker pull reshmimahadevan/gorest:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                bat 'if not exist newman mkdir newman'
                bat 'docker run -v %cd%\\newman:/app/newman reshmimahadevan/gorest:1.0'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: '*.html',
                    reportName: 'HTML Extra API Report',
                    reportTitles: ''
                ])
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
