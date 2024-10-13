pipeline{
    
    agent any
    stages{
        
    stage("code"){
        steps{
            echo "Code clone is done"
            git url: "https://github.com/LondheShubham153/django-notes-app.git", branch: "main"
        }
    }
    
    stage("build"){
        steps{
            echo "code build is done"
            sh "docker build . -t django_note_app:latest"
        }
      }
     
    stage("Push") {
    steps {
        echo "Pushing code to Dockerhub"
        withCredentials([usernamePassword(credentialsId: "dockerhub", usernameVariable: "dockerhubUser", passwordVariable: "dockerhubPass")]) {
            sh "docker tag django_note_app ${env.dockerhubUser}/django_note_app:latest"
            sh """ echo ${env.dockerhubPass}|docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"""
            sh "docker push ${env.dockerhubUser}/django_note_app:latest"
        }
    }
}

stage('Deploy'){
    steps{
       sh "docker compose down && docker compose up -d"
        echo "code deployed successfully"
    }
}
    }
}
