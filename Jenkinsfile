node{
  stage('GIT Checkout'){ 
    checkout([
             $class: 								'GitSCM', 
             branches:  							[[name: '*/master']],
             doGenerateSubmoduleConfigurations: 	false,
             extensions: 							[],
             submoduleCfg:							[],
             userRemoteConfigs:						[[credentialsId: 'jenkins-ssh', url: 'git@github.com:anatol11k/Prj1.git']]])
                                                                                                                          }
    
  stage('Build Package'){
    sh 'cd spring-boot-sample-web-ui/ && mvn clean install '
                                                                                                                          }
  
  }
  
  
