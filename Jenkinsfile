node{
    tool name: 'Maven382', type: 'maven'
    
    stage("Git Checkout"){
        git 'https://github.com/oktbabs/spring-boot-mongo-docker.git'
        
    }
    stage("Maven Clean Build"){
        sh 'mvn clean package'
        
    }
    stage("Build Docker Image"){
        sh 'sudo docker build -t  jenkinserver.mycompany.com:8085/spring-boot-mongo .'
        
    }
/**    stage("Connect to nexus"){
        withCredentials([usernamePassword(credentialsId: 'NEXUS-REPO-CREDS', passwordVariable: 'Kala8Kuta', usernameVariable: 'admin')]) {
        sh "sudo docker login -u ${NEXUS-REPO-CREDS} -p ${NEXUS-REPO-CREDS} jenkinserver.mycompany.com:8085"
}
          
                sh 'sudo docker push jenkinserver.mycompany.com:8085/spring-boot-mongo'
    }
    */
    
    stage("Connect to nexusartefactuploader"){    
    nexusArtifactUploader artifacts: [[artifactId: 'spring-boot-mongo', classifier: '', file: 'target/spring-boot-mongo', type: 'war']], credentialsId: 'NEXUS3-REPO-CREDS', groupId: 'com.mt', nexusUrl: 'jenkinserver.mycompany.com:8085', nexusVersion: 'nexus3', protocol: 'http', repository: 'timmyfirstnexus', version: '1.0'
}
}
