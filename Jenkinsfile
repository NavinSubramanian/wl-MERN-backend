pipeline {
    agent any
    tools {
        nodejs 'Nodejs'
    }
    environment {
        PATH = 'C:\\WINDOWS\\SYSTEM32'
        NODEJS_PATH = 'C:\\Program Files\\nodejs'
        SONAR_SCANNER_PATH = 'C:\\Users\\nnavi\\OneDrive\\Desktop\\sonar-scanner-cli-6.2.1.4610-windows-x64\\sonar-scanner-6.2.1.4610-windows-x64\\bin'
    }

    stages {
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                script {
                    bat '''
                        set PATH=%NODEJS_PATH%;%PATH%
                        npm install
                        npm run build
                    '''
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    bat '''
                        set PATH=%NODEJS_PATH%;%SONAR_SCANNER_PATH%;%PATH%
                        sonar-scanner -Dsonar.projectKey=mern1-backend ^
                                      -Dsonar.sources=. ^
                                      -Dsonar.exclusions="**/node_modules/**,**/.env" ^
                                      -Dsonar.host.url=http://localhost:9000 ^
                                      -Dsonar.token=sqp_f6c64e7b66028a7288f81b1c57e77b696f8bd975
                    '''
                }
            }
        }
    }

    post {
        success {
            echo "SonarQube analysis complete"
        }
        failure {
            echo "SonarQube analysis failed"
        }
    }
}
