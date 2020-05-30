properties([
    [
            $class  : 'BuildDiscarderProperty',
            strategy: [$class               : 'LogRotator',
                       artifactDaysToKeepStr: '14',
                       artifactNumToKeepStr : '5',
                       daysToKeepStr        : '',
                       numToKeepStr         : '10'
                       ]
    ], disableConcurrentBuilds()
    ])

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
  
  
