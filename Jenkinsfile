pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/suresh-akidev/terraform-jenkins']]])            

          }
        }
        
        // stage ("Build Docker Image") {
        //     steps {
        //         sh ('sudo docker build --tag thala-app .') 
        //         //sh ('sudo docker tag thala-app:latest thala-app:v1.0.0') 
        //     }
        // }

        // stage ("Push Docker Image") {
        //     steps {
        //         sh ('aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 157673692367.dkr.ecr.us-east-1.amazonaws.com') 
        //         sh ('sudo docker tag thala-app:latest 157673692367.dkr.ecr.us-east-1.amazonaws.com/app-repo:latest')
        //         sh ('sudo docker push 157673692367.dkr.ecr.us-east-1.amazonaws.com/app-repo:latest')
        //     }
        // }

        stage ("terraform init") {
            steps {
                sh ('cd terraform_resources')
                sh ('terraform init') 
            }
        }
        stage ("terraform validate") {
            steps {

                echo "Terraform action is --> validate"
                sh ('cd terraform_resources')
                sh ('terraform validate') 
           }
        }
        stage ("terraform plan") {
            steps {
                echo "Terraform action is --> plan"
                sh ('cd terraform_resources')
                sh ('terraform plan') 
           }
        }

        stage ("terraform apply") {
            steps {
                echo "Terraform action is --> apply"
                sh ('cd terraform_resources')
                sh ('terraform apply --auto-approve -var-file dev.tfvars' ) 
           }
        }
    }
}