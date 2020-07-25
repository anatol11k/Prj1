properties([
    [
            $class  : 'BuildDiscarderProperty',
            strategy: [$class               : 'LogRotator',
                       artifactDaysToKeepStr: '13',
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
      sh 'pwd'
      sh 'mv spring-boot-sample-web-ui/target/*.jar ./web-ui.${BUILD_NUMBER}.jar'
      nexusArtifactUploader artifacts:
          [[artifactId: 'web-ui.${BUILD_NUMBER}',
            classifier: '',
            file: 'web-ui.${BUILD_NUMBER}.jar', 
            type: 'jar']],
          credentialsId: 'Nexus-Jenkins',
          groupId: 'gradwork.web_ui',
          nexusUrl: '3.123.21.171:8081',
          nexusVersion: 'nexus3',
          protocol: 'http',
          repository: 'Jenkins',
          version: '1.0'
            }
      
    stage('Archieve Artifact'){   
 
       def userInput = input(
       id: 'userInput', message: 'Port for application to run', parameters: [
       [$class: 'TextParameterDefinition',
       defaultValue: '8000',
       description: 'Port',
       name: ''] ])
       def PORT = userInput
        
       archiveArtifacts(
         artifacts: '*.jar', 
         followSymlinks: false,
         fingerprint: true
           )
       build( 
         job: 'GW_Deploy',
           parameters: [
         string(
         name: 'JV',
         value: String.valueOf(BUILD_NUMBER)),
         string(
         name: 'PORT',
         value: PORT)
       ]
           )
  }
}
