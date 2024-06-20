pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from your Git repository
                git branch: 'main', url: 'https://github.com/Pavan0445/Jenkins_Test.git'
            }
        }

        stage('Terraform Init, Plan and Apply') {
            steps {
                script {
                    // Set the AWS credentials environment variables for Terraform
                    withEnv(["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}"]) {
                        sh '''
                            # Initialize Terraform
                            terraform init
                            
                            # Plan the Terraform deployment
                            terraform plan -out=tfplan
                            
                            # Apply the Terraform deployment
                            terraform apply -auto-approve tfplan
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up the workspace after the build
            cleanWs()
        }
   
