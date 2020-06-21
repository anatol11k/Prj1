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
    
     stage("Clean"){
        sh "uptime"
        deleteDir()
                    }
    
    
  stage('GIT Checkout'){ 
    checkout([
             $class: 								'GitSCM', 
             branches:  							[[name: '*/master']],
             doGenerateSubmoduleConfigurations: 	false,
             extensions: 							[],
             submoduleCfg:							[],
             userRemoteConfigs:						[[credentialsId: 'Jenkins_git', url: 'git@github.com:anatol11k/Prj1.git']]])
                                                                                                                          }
    
  stage('Build Package'){
    sh 'cd spring-boot-sample-web-ui/ && mvn clean install '
                                                                                                                         }
  stage('Upload Artifact'){
      
      sh 'mv spring-boot-sample-web-ui/target/*.jar ./web-ui.${BUILD_NUMBER}.jar'
      
       archiveArtifacts(
         artifacts: '*.jar', 
         followSymlinks: false,
         fingerprint: true
           )
       build( 
       job: 'GW_Deploy',
       parameters:
       [string(
       name: 'JV',
       value: String.valueOf(BUILD_NUMBER))]
           )
                                                                                                                           }

}
  
  
