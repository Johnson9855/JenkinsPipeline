pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
               sh 'mvn test'
            }
        }
        
        stage('Code Analysis') {
            steps {
               sh 'sonar-scanner'
            }
        }
        
        stage('Security Scan') {
            steps {
                sh 'sonar-scanner -Dsonar.qualitygate.wait=true'
            }
        }
        
        stage('Deploy to Staging') {
            steps {
               sh 'aws ecs update-service --cluster your-cluster-name --service your-service-name --force-new-deployment'
            }
        }
        
        stage('Integration Tests on Staging') {
            steps {
                sh 'newman run your-api-tests.postman_collection.json'
            }
        }
        
        stage('Deploy to Production') {
            steps {
                sh 'aws ecs update-service --cluster your-cluster-name --service your-service-name --force-new-deployment'
            }
        }
    }
    
    post {
        success {
            emailext (
                subject: "Pipeline Successful",
                body: "Your Jenkins pipeline has completed successfully.",
                to: "johnson9855@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "Pipeline Failed",
                body: "Your Jenkins pipeline has failed. Please check the logs for details.",
                to: "johnson9855@gmail.com"
            )
        }
    }
}
