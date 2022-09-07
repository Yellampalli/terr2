pipeline {
    agent any
    parameters {
        choice(name: 'action', choices: 'create\ndestroy', description: 'Create/update or destroy the server')
    }
    stages {
        stage('Cloning') {
            steps {
                git 'https://github.com/Yellampalli/terr2.git'
            }
        }
        stage('TF Plan') {
            when {
                expression { params.action == 'create' }
            }
            steps {
                script {
                        sh """
                        ls -l
                        pwd
                        hostname
                        terraform init
                        terraform plan
                        """
                    }
                }
        }
        stage('TF Apply') {
          when {
            expression { params.action == 'create' }
          }
          steps {
            script {
                        sh """ 
                        terraform apply -input=false -auto-approve
                        """
                    }
                }
        }
        stage('TF Destroy') {
          when {
            expression { params.action == 'destroy' }
          }
          steps {
            script {
                        sh """ 
                        terraform destroy -auto-approve
                        """
                    }
                }
        }
    }        
}
