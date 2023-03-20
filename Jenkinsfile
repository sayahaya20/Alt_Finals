pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_DEFAULT_REGION = "us-east-1"
    }
    stages {
        stage("Create nginx-conroller") {
            steps {
                script {
                    dir('Altschool_Exam/nginx-controller') {
                       sh "aws eks --region us-east-1 update-kubeconfig --name demo"
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }

        stage("Create prometheus") {
            steps {
                script {
                    dir('Altschool_Exam/prometheus') {
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }

        stage("Deploy voting-app to EKS") {
            steps {
                script {
                    dir('Altschool_Exam/vote-app') {
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }

        stage("Deploy sock-shop to EKS") {
            steps {
                script {
                    dir('Altschool_Exam/sock-shop-app') {
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }

        stage("Deploy ingress rule to EKS") {
            steps {
                script {
                    dir('Altschool_Exam/ingress-rule') {
                        sh "terraform init"
                        sh "terraform apply -auto-approve"
                    }
                }
            }
        }
    }
}
