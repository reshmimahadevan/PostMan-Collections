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
                bat 'docker run -v %cd%/newman:/app/newman reshmimahadevan/gorestapi:1.0'
}
        }

        stage('Verify Reports') {
            steps {
                bat 'dir C:\\Users\\reshm\\.jenkins\\workspace\\PostManWithPipelineProject\\newman'
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
        archiveArtifacts artifacts: 'newman/*', allowEmptyArchive: true
    }
}


}
