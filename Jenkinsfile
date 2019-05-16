pipeline {
    agent any
    options { disableConcurrentBuilds() }
    parameters {
        string(defaultValue: 'True', description: '"True": push docker image after pull; otherwise leave empty', name: 'pushimage')
    }

    stages {
        stage('Pull') {
            steps {
                sh 'docker pull centos:7'
            }
        }
        stage('Tag') {
            steps {
                sh '''
                    docker tag centos:7 intra/centos7_base
                    if [[ "$DOCKER_REGISTRY_USER" ]]; then
                        echo "Docker registry user: $DOCKER_REGISTRY_USER"   # defined in Jenkins env
                        docker tag centos:7 $DOCKER_REGISTRY_USER/centos7_base
                    fi
                '''
            }
        }
       stage('Push ') {
            when {
                expression { params.pushimage?.trim() != '' }
            }
            steps {
                sh '''
                    if [[ "$DOCKER_REGISTRY_USER" ]]; then
                        docker push $DOCKER_REGISTRY_USER/centos7_base
                    else
                        docker push centos7_base
                    fi
                '''
            }
        }
    }
}
