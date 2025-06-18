pipeline {
  agent any
  environment {
    AWS_REGION = 'us-east-1'
  }
  stages {
    stage('Terraform Init') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh '''
            terraform init
          '''
        }
      }
    }
    stage('Terraform Format & Validate') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh '''
            terraform fmt -check
            terraform validate
          '''
        }
      }
    }
    stage('Terraform Plan') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh '''
            terraform plan
          '''
        }
      }
    }
    stage('Terraform Apply') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'aws-creds', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
          sh '''
            terraform apply -auto-approve
          '''
        }
      }
    }
  }
}
