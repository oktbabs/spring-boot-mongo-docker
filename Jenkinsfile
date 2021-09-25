node{
    tool name: 'Maven382', type: 'maven'
    
    stage("Git Checkout"){
        git 'https://github.com/oktbabs/spring-boot-mongo-docker.git'
        
    }
    stage("Maven Clean Build"){
        sh 'mvn clean package'
        
    }
    stage("Build Docker Image"){
        sh 'sudo docker build -t timmyfirstnexus/spring-boot-mongo .'
        
    }
    stage("Push to docker image to nexus"){
        withCredentials([usernameColonPassword(credentialsId: 'NEXUS-REPO-CREDS', variable: 'NEXUS-REPO-CREDS')]) {
              
            sh "sudo docker login -u admin -p ${NEXUS-REPO-CREDS} -U http://jenkinserver.mycompany.com:8085"
          }
        
        sh 'sudo docker push timmyfirstnexus/spring-boot-mongo'
        
    }

}

