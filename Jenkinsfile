pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                git branch: 'master', credentialsId: 'github', url: 'https://github.com/uchanbi/test-app.git'
                sh 'mvn clean package'
            }
        }
        stage('verify') {
            steps {
                sh 'ls -alF target'
            }
        }        
        stage('docker') {
                withDockerRegistry([credentialsId: 'docker-hub', url: 'https://hub.docker.com']) {
                    def app = docker.build("bihanc/jenkins",'.')
                    app.push()
                }
        }
    }
}
