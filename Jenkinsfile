pipeline {
    agent any

    environment {
        RUST="/var/lib/jenkins/.cargo/bin"
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetching source code from https://github.com/GhostUponAvon/6.1C.git"
                echo 'Building for Linux'
                dir("app") {
                    sh "$RUST/cargo build"
                    
                }
                echo "built 'app'"
                
            }
        }
        stage('Test') {
            steps {
                echo "Running Unit Tests"
                dir("app") {
                    sh "$RUST/cargo test"
                    
                }

            }
            post {
                success {
                    echo "Testing executed successfully"
                    emailext attachLog: true, body: 'The testing was: successfully', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Testing'
                }
                failure {
                    echo "Testing failed"
                    emailext attachLog: true, body: 'The testing has: failed', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Testing'
                }
            }
        }
        stage('Code Quality Check') {
            steps {
                echo "Running code quality checks"
                dir("app") {
                    sh "$RUST/cargo clippy"
                    
                }
            }
        }
        stage('Security Scan') {
            steps {
                echo "Scanning for security flaws with sast-scan cdxgen (https://github.com/ShiftLeftSecurity/sast-scan.git)"

            }
            post {
                success {
                    echo "Security scan executed successfully"
                    emailext attachLog: true, body: 'The security scan was: successfully', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Security'
                }
                failure {
                    echo "Security scan failed"
                    emailext attachLog: true, body: 'The security scan has: failed', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Security'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying to staging server"
            }
        }
        stage('Integration Testing') {
            steps {
                echo "Performing Integration testing"
                sleep 10
            }
            post {
                success {
                    echo "Integration testing executed successfully"
                    emailext attachLog: true, body: 'The integration testing was: successfully', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Integration'
                }
                failure {
                    echo "Integration testing failed"
                    emailext attachLog: true, body: 'The integration testing has: failed', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status: Integration'
                }
            }
        }
        stage('Deploy to Production') {
            steps {
                echo "Pushing to Production Enviroment"
            }
        }
        
    }
    post {
        always {
            echo "Pipeline Finished"
        }
        success {
            echo "Pipeline executed successfully"
            emailext attachLog: true, body: 'The pipeline has built: successfully', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status'
        }
        failure {
            echo "Pipeline execution failed"
            emailext attachLog: true, body: 'The pipeline build has: failed', to:'mikehodgetheboss@gmail.com', subject: 'Pipeline build status'
        }
    }
}
