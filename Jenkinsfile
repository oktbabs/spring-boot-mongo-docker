node{
    tool name: 'Maven382', type: 'maven'
    
    stage("Git Checkout"){
        git 'https://github.com/oktbabs/spring-boot-mongo-docker.git'
        
    }
    stage("Maven Clean Build"){
        sh 'mvn clean package'
        
    }
    stage("Build Docker Image"){
        sh 'docker build -t oktbabs/spring-boot-mongo:1.0 .'
        
    }
    stage("Push image to DockerHub"){
    withCredentials([string(credentialsId: 'DOCKER_HUB_CRED', variable: 'DOCKER_HUB_CRED')]) {
       sh "docker login -u oktbabs -p ${DOCKER_HUB_CRED}"
       }
           
        sh "docker push  oktbabs/spring-boot-mongo:1.0"
        
    }

    stage("Deploy application to kubernetes"){
        kubernetesDeploy(
		configs: 'springBootMongo.yml',
		kubeconfigId: 'KUBERNETES_CLUSTER_CONFIG',
         enableConfigSubstitution: true		
        )
    }
}
