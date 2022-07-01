  pipeline {
    agent {
      node {
        label "master"
      } 
    }

    stages {
      stage('fetch_latest_code') {
        steps {
          git url: 'https://github.com/Omidznlp/Terraform-Jenkins.git'
        }
      }

      stage('TF Init&Plan') {
        
        steps {
          withAWS(credentials: 'terraform-credentials') {
          sh 'terraform -chdir=terraform init'
          sh 'terraform -chdir=terraform plan'
          }
        }
              
      }

      stage('Approval') {
        steps {
          script {
            def userInput = input(id: 'confirm', message: 'Apply Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Apply terraform', name: 'confirm'] ])
          }
        }
      }

      stage('TF Apply') {
        steps {
          withAWS(credentials: 'terraform-credentials') {
          sh 'terraform -chdir=terraform apply -input=false --auto-approve'
          }
        }
      }
      stage('Removal') {
        steps {
          script {
            def userInput = input(id: 'confirm', message: 'Destroy Terraform?', parameters: [ [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Destroy terraform', name: 'confirm'] ])
          }
        }
      }

      stage('TF Destroy') {
        steps {
          withAWS(credentials: 'terraform-credentials') {
          sh 'terraform -chdir=terraform destroy -input=false --auto-approve'
          }
        }
      }
    } 
  }