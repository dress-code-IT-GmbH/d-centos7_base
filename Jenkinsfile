pipeline {
    agent any
    stages {
        stage('Pull') {
            steps {
                sh 'docker pull centos:7'
            }
        }
        stage('Tag') {
            steps {
                sh 'docker tag centos:7 intra/centos:7'
            }
        }
    }
}