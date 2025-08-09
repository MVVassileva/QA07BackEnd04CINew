pipeline {
    agent any

    environment {
        NODE_VERSION = '18.x'
    }

    tools {
        nodejs "${NODE_VERSION}"
    }

    stages {
        stage('Checkout'){
            steps{
                checkout scm     
            }
        }

        stage("Install dependencies"){
            steps{
                script{
                    if(isUnix){
                        sh 'npm install'
                    }
                    else {
                        sh 'npm install '
                    }
                }
            }
        }

        stage("Start application and run tests"){
            steps{
                scrip{
                    sh 'npm start &'
                    sh 'wait-on http://localhost:8080'
                    sh 'npm test'
                }
            }
        }
    }

    post {
        always {
            echo "CI pipeline completed."
        }
    }
}