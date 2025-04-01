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
                bat 'docker pull reshmimahadevan/gorestapi:1.0'
            }
        }

        stage('Run API Test Cases') {
            steps {
                bat 'docker run --rm -v "C:/jenkins/workspace/myjob/newman:/app/results" reshmimahadevan/gorestapi:1.0'
            }
        }

        stage('Verify Reports') {
            steps {
                bat 'dir C:/jenkins/workspace/myjob/newman'
            }
        }

        stage('Publish HTML Extra Report') {
            steps {
                publishHTML([ 
                    allowMissing: false,
                    alwaysLinkToLastBuild: false,
                    keepAll: true,
                    reportDir: 'newman',
                    reportFiles: 'gorest.html',
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
    
    post {
        always {
            archiveArtifacts artifacts: 'newman/*.json', allowEmptyArchive: true
        }
    }
}
