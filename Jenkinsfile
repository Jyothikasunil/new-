pipeline {
    agent any

    triggers {
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checkout the code from the GitHub repository"
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                    userRemoteConfigs: [[url: 'https://github.com/veena223070113/Jenkins_6.2C.git']]
                ])
            }
        }

        stage('Build') {
            steps {
                echo "Build the code using Maven"
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Run unit tests"
                sh 'mvn test'

                echo "Run integration tests"
                echo "Integration test using Postman"
                // Add actual Postman command or script here
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Integrate SonarQube"
                echo "Code Analysis using SonarQube analysis command"
                // Add actual SonarQube analysis command here
            }
        }

        stage('Security Scan') {
            steps {
                echo "Run security scan using OWASP ZAP"
                echo "Security scan using OWASP ZAP"
                // Add actual OWASP ZAP command here
            }
            post {
                success {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Security Scan Successful",
                        body: "The security scan was successful. Check the attached logs for details.",
                        attachLog: true
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Security Scan Failed",
                        body: "The security scan failed. Check the attached logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying the application to staging server using AWS CodeDeploy"
                // Add actual AWS CodeDeploy command here
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests on the staging environment"
                echo "Using Selenium for UI tests and JMeter for performance tests"
                // Add actual Selenium and JMeter commands here
            }
            post {
                success {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Staging Tests Successful",
                        body: "The integration tests on the staging environment were successful. Check the attached logs for details.",
                        attachLog: true
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Staging Tests Failed",
                        body: "The integration tests on the staging environment failed. Check the attached logs for details.",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying the application to production server using AWS CodeDeploy"
                // Add actual AWS CodeDeploy command here
            }
            post {
                success {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Deployment to Production Successful",
                        body: "The deployment to the production server was successful. Check the attached logs for details.",
                        attachLog: true
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'logs/*', allowEmptyArchive: true
                    emailext(
                        to: "jyothikasunil006@gmail.com",
                        subject: "Deployment to Production Failed",
                        body: "The deployment to the production server failed. Check the attached logs for details.",
                        attachLog: true
                    )
                }
            }
        }
    }

    post {
        always {
            echo "Sending a notification email"
            emailext(
                subject: "Pipeline ${currentBuild.result}",
                body: "The pipeline has completed with status: ${currentBuild.result}.",
                to: "specified-email@example.com",
                attachLog: true
            )
        }
    }
}
