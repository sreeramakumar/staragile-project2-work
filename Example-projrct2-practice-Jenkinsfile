pipeline {
    agent any

    stages {
        stage('clone git url') {
            steps {
                git 'https://github.com/sreeramakumar/Example-projrct2-practice.git'
            }
        }
        stage('docker image build and push to docker hub') {
            steps {
                sh "chmod 400 de2.pem"
                sh "sleep 10"
                sh 'ansible all -i inventory.yaml -m ping --private-key=de2.pem -u ec2-user'
                sh 'ansible-playbook -i inventory.yaml --private-key=de2.pem -u ec2-user dockerimagebuild.yaml'
            }
        }
        stage('docker installing on docker server') {
            steps {
                sh "chmod 400 de2.pem"
                sh "sleep 10"
                sh 'ansible all -i inventory2.yaml -m ping --private-key=de2.pem -u ec2-user'
                sh 'ansible-playbook -i inventory2.yaml --private-key=de2.pem -u ec2-user dockerinstall.yaml'
            }
        }
        stage('deploy application on docker server') {
            steps {
                sh 'ansible all -i inventory2.yaml -m ping --private-key=de2.pem -u ec2-user'
                sh 'ansible-playbook -i inventory2.yaml --private-key=de2.pem -u ec2-user deployapplication2.yaml'
            }
        }
    }
}
