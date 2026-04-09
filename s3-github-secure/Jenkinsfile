pipeline {
    agent any

    environment {
        PATH = "/home/codespace/.python/current/bin:$PATH"
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Checkout Code') {
            steps {
              checkout scm
            }
        }
        stage('Check Ansible and AWS version'){
            steps{
                sh 'ansible --version'
                sh 'aws --version'
            }
        }
      
        stage('Run Ansible Playbook') {
            steps {
                withCredentials([usernamePassword(credentialsId:'git',usernameVariable:'GIT_USERNAME',passwordVariable:'GIT_TOKEN')]){
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws_credentials']]) {
                // Run your Ansible playbook
                sh '''
                ansible-playbook copy_JarToS3.yml
                '''
                }    
            }
            }
        }
    }

    post {
        always {
            // Archive the logs
            archiveArtifacts artifacts: '**/*.log', allowEmptyArchive: true
        }
    }
}
