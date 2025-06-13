pipeline{
    agent any

    stages{
        stage("Checkout"){
            steps{
                checkout scm
            }
        }
        stage('Check or Install Node.js') {
                    steps {
                        bat '''
                        where node >nul 2>nul
                        if %ERRORLEVEL% NEQ 0 (
                            echo Node.js not found, downloading...
                            curl -o %NODE_INSTALLER% %NODE_URL%
                            msiexec /i %NODE_INSTALLER% /quiet /norestart
                        ) else (
                            echo Node.js is already installed.
                        )
                        node -v
                        npm -v
                        '''
                    }
        }

        stage("Install dependencies"){
            steps{
                bat 'npm install'
            }
        }

        stage("Start server"){
            steps{
                    bat 'npm start -- --port 8081'
                }
        }

        stage("Run tests"){
            steps{
                bat 'npm test'
            }
        }
    }
}