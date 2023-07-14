pipeline {
    agent any

    stages {

        stage ('Terraform Init'){
            
            steps {
                
                dir('./Jenkins_Ec2') {
                    
                    sh '/usr/local/bin/terraform init'
                }
            }
        }

        stage ('Terraform Plan'){
            
            steps{
                
                dir('./Jenkins_Ec2'){
                    
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
                
                dir('./Jenkins_Ec2') {
                    
                    sh '/usr/local/bin/terraform apply -auto-approve'
                }
            }
        }
    }
}
