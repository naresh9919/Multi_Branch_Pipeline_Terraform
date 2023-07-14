pipeline {
    agent any

    stages {
        stage ('checkout SCM'){
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/naresh9919/Multi_Branch_Pipeline_Terraform.git'
            }
        }

        stage ('Terraform Init'){
            steps {
                script {
                    sh '/usr/local/bin/terraform init'
                }
            }
        }

        stage ('Terraform Plan'){
            steps{
                script{
                    sh '/usr/local/bin/terraform plan'
                }
            }
        }
        
        stage ("Approvel"){
            when {branch 'main'}
            steps{
                script{
                   waituntill {
                    fileExists('dummyfile')
                   }
                }
            }
        }

        stage ("Terraform Apply") {
            steps {
                script {
                    sh '/usr/local/bin/terraform apply -auto-approve'
                }
            }
        }
    }
}
