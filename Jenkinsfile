
pipeline {
  agent any
  
  environment {
    DIRECTORY_PATH = "/Users/adhishanand/.jenkins/jobs/"
    TESTING_ENVIRONMENT = "Development"
    PRODUCTION_ENVIRONMENT = "Production"
  }

  triggers {
    pollSCM('H/2 * * * *')
  }
  
  stages {
    stage('Build') {
      steps {
        echo "Build the code using a build automation tool such as Maven to compile and package "
      }
    }
    
    stage('Unit and Integration Test') {
      steps {
        echo "Run unit tests"
        echo "Run integration tests using JUnit, Mockito or Selenium"
      }
    }
    
    stage('Code Analysis') {
      steps {
        echo "Use sonar qube to analyse the code"
      }
    }
    
    stage('Security Scan') {
      steps {
        echo "For security scan sonar qube can be used."
      }
      post {
        always {
          emailext attachLog: true, body: "Security scan completed with ${currentBuild.currentResult}", recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: "Pipeline ${currentBuild.currentResult} - ${env.JOB_NAME}"
        }
    }
    }
    
    stage('Deploying to Staging') {
      steps {
        echo 'AWS EC or AWS EKS can be used for deployment to staging.'
      }
    }
    
    stage('Integration Test on Staging') {
      steps {
        echo "Deploying the code to the ${env.PRODUCTION_ENVIRONMENT} environment"
      }
      post {
        always {
          emailext attachLog: true, body: "Integration Test completed with ${currentBuild.currentResult}", recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: "Pipeline ${currentBuild.currentResult} - ${env.JOB_NAME}"
        }
      }
    }
    
    stage('Deploy to Production') {
      steps {
        echo 'AWS EC or AWS EKS can be used for deployment to production.'
      }
    }
  }
}

