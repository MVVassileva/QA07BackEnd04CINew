pipeline {
    agent any

    environment {
        NODE_VERSION = '18.x'
    }

//    tools {
//        nodejs "${NODE_VERSION}"
//    }

    stages {
        stage('Checkout'){
            steps{
                checkout scm     
            }
        }

        stage('Setup Node.js') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            if ! command -v node &> /dev/null; then
                                echo "Node.js not found, installing..."
                                curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
                                sudo apt-get install -y nodejs
                            fi
                            node --version
                            npm --version
                        '''
                    } else {
                        bat '''
                            node --version
                            npm --version
                        '''
                    }
                }
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
            echo "CI pipeline completed"
        }
    }
}