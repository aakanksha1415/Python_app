pipeline {
  agent any

  stages {
    stage('Check-out') {
      steps {
        git url: "https://github.com/aakanksha1415/project.git", branch: "main"
        echo "HI CLonned code"
      }
    }
    
    stage('Build Image'){
        steps{
          
            sh ' docker build -t my-python-app:latest .'
            
        }
    }
    
    stage("Publish Image"){
            steps{
                withCredentials([usernamePassword(credentialsId:"docker-hub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker tag my-python-app:latest ${env.dockerHubUser}/my-python-app:latest"
                sh "docker push ${env.dockerHubUser}/my-python-app:latest"
          
                }
            }
        }
    }
}  
   