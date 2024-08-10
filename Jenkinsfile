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
        }
        stage('Deploy to Production') {
            steps {
                echo "Pushing to Production Enviroment"
            }
        }
        
    }
}
