pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage('Checkout') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-int-jenkins', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    git credentialsId: 'github-int-jenkins', url: 'https://github.com/slalit28/Aaptatt-hiring-assignment.git', branch: 'master'
                }
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -B -f pom.xml clean install package'
            }
        }
        stage('DockerImage') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD} docker.io"
                sh 'docker build -t blackhat0007/devops:latest -f Dockerfile .'
                sh 'docker push blackhat0007/devops:latest'
            }
        }
    }
}
}
