pipeline {
    agent any
    
    stages {
        stage("Build") {
            steps {
                echo "Compile the code and generate any necessary artifacts."
                echo "Code built using a build automation tool called Maven."
            }
        }
        
        stage("Unit and Integration Tests") {
            steps {
               echo "Unit tests."
                echo "Integration tests."
                echo "pytest was the tool use for this."
            }
        }
            post {
                always {
                    mail to: "s223565746@deakin.edu.au",
                        subject: "Test status: ${currentBuild.result}",
                        body:"The test stage has completed. Status: ${currentBuild.result}"
                }
            }
    }
        
        stage("Code Analysis") {
            steps {
               echo "Check quality of the code"
                echo "SonarQube was the tool used for this"
            }
        }
        
        stage("Security Scan") {
            steps {
                echo " Perform a security scan on the code using QWASP ZAP."
            }
            post {
                always {
                    mail to: "s223565746@deakin.edu.au"
                    subject: "Security scan status: ${currentBuild.result}"
                    body: "The security scan stage has completed. Status: ${currentBuild.result}"
                }
            }
        }
        
        stage("Deploy") {
            steps {
               echo "Deploy the application to a staging server (e.g., AWS EC2 instance) using Jenkins."
            }
        }
        
        stage("Integration Tests on Staging") {
            steps {
                echo "run integration tests on the staging environment to ensure the application functions as expected in a production-like environment"
                sleep 10
            }
        }
        
        stage("Deploy to Production") {
            steps {
                echo "The product $PRODUCTION_ENVIRONMENT is ready for production"
                echo "deploy the application to a production server (e.g., AWS EC2 instance) using Jenkins."
            }
            post {
                always {
                    mail to: "s223565746@deakin.edu.au"
                    subject: "Security scan status: ${currentBuild.result}"
                    body: "The security scan stage has completed. Status: ${currentBuild.result}"
                }
            }
        }
}
