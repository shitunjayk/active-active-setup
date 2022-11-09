pipeline {
  agent any
  stages {
    stage("Git Checkout") {
      steps {
        script {
          git branch: 'main', credentialsId: 'azure-blog-cred', url: 'https://gitlab.com/shitunjay.opstree/azure-blog.git'
        }
      }
    }

     stage("Parameter Setup") {
      steps {
        script {
        properties([
          parameters([
            choice(choices: ['apply', 'destroy'], name: 'ACTION')])])
        }
      }
    }


    stage("Terraform Init") {
      steps {
        script {
          dir('region-1/') {
            sh 'terraform init'
          }
          dir('region-2/') {
            sh 'terraform init'
          }
        }
      }
    }
    stage("Terraform Validate") {
      steps {
        script {
          dir('region-1/') {
            sh 'terraform validate'
          }
          dir('region-2/') {
            sh 'terraform validate'
          }
        }
      }
    }
    stage('Terraform Plan') {
      steps {
        script {
          dir('region-1/') {
            sh 'terraform plan'
          }
          dir('region-2/') {
            sh 'terraform plan'
          }
        }
      }
    }
    stage('Terraform Approval') {
      steps {
        script {
          def userInput = input(id: 'confirm', message: 'Approve Terraform ?', parameters: [
            [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Approve Terraform', name: 'confirm']
          ])
        }
      }
    }
    stage('Terraform Action') {
      steps {
        script {
          dir('region-1/') {
            sh 'terraform $ACTION --auto-approve'
          }
          dir('region-2') {
            sh 'terraform $ACTION --auto-approve'
          }
        }
      }
    }
  }
}
