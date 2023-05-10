node {
    
  stage('git clone') {
      
    git branch: 'main', credentialsId: 'gitlab', url: 'git@gitlab.com:formation_09_2022/projet1_j2e.git'
}
     
  stage('build'){
    sh 'mvn clean install package'
  }

  stage('upload Artifact to Nexus'){
   
   nexusArtifactUploader artifacts:[[artifactId: 
   'maven-project', 
    classifier: '',
    file: 'webapp/target/webapp.war', 
    type: 'war']], 
    credentialsId: 'nexus', 
    groupId: 'com.example.maven-project', 
    nexusUrl: '13.39.86.54:8081', 
    nexusVersion: 'nexus3', 
    protocol: 'http', 
    repository: 'projet1_j2e', 
    
    version: "version '${env.JOB_NAME} [${env.BUILD_NUMBER}]'" 

  }



  stage("deploy"){
      
    deploy adapters: [tomcat8(credentialsId: 'tomcat', path: '', url: 'http://13.36.195.131:8080')], contextPath: null, war: '**/*.war'
}
}
