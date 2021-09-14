pipeline {
    environment {
    imagename = "nginx"
  }
    agent any
	stages {
        stage('Cloning repository from Git') {
            steps{
                script{
                    checkout scm
        }}}

        stage('Building image') {
            steps{
                script {
                  def app = docker.build("$imagename")
    } } }

        stage('Pushing image to Docker-Hub') {
            steps{
                script{
		    def app 
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-id') {
                    app.push("v1.${env.BUILD_NUMBER}")
                    app.push("latest")
                }
                } 
        } }

        stage('docker image clean up'){
            steps{
                script{
                sh "docker rmi $imagename:$BUILD_NUMBER"
                sh "docker rmi $imagename:latest"
        }
        }
        }

        stage('Ansible Book'){
            steps{
                script{
                    def image_id = registry + ":$BUILD_NUMBER"
                    sh "ansible-playbook  Ansible-playbook.yml --extra-vars \"image_id=${image_id}\""
                    ansiblePlaybook become: true, installation: 'Ansible-Belt3', inventory: 'hosts', playbook: 'Ansible-playbook.yml'
                }
            }
        }
}
 }
