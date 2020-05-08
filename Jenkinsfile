pipeline {
    agent {
        label 'docker'
    }
    stages {
        stage('Build') {
            steps {
                sh "docker build --tag ${GIT_COMMIT} ."
            }
        }
        stage('Publish') {
            when {
                branch 'master'
            }
            steps {
                sh "docker tag ${GIT_COMMIT} fint/hub:latest"
                withDockerRegistry([credentialsId: 'asgeir-docker', url: '']) {
                    sh "docker push fint/hub:latest"
                }
            }
        }
    }
}
