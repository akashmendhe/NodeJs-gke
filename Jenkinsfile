pipeline {
    agent any

    stages {
        stage("Git Clone"){
            steps{
                git url: "https://github.com/akashmendhe/NodeJs-gke.git", branch: "master"
            }
        }
        stage("Create Docker Image"){
            steps{
		    echo "Build and Test"
		    withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker build -t akashm123/hello-gke:$BUILD_NUMBER ."
					}
            }
        }
         stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker images"
		    sh "docker push akashm123/hello-gke:$BUILD_NUMBER"
				}
			}
		}
        stage('Deploy to GKE') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }
    }
}
