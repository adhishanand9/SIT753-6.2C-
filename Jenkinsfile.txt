
pipeline {
  agent any
  
  environment {
    DIRECTORY_PATH = "/Users/adhishanand/.jenkins/jobs/"
    TESTING_ENVIRONMENT = "Development"
    PRODUCTION_ENVIRONMENT = "Production"
  }

  triggers {{
    pollSCM('H/2 * * * *')
  }}
  
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
          mail to : "adhishanand9@gmail.com",
          subject : "Job '${env.JOB_NAME}'- (${env.BUILD_NUMBER}) has PASSED",
          body : "build is complete successfully"
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
        success {
          echo "Build Successfully deployed to both environments"
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
