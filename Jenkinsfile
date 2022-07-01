pipeline{
  
  agent any
  
  environment {
           
            mvnCMD = "/usr/share/maven/bin/mvn"
            exec = "cd /opt/docker; sudo ansible-playbook build.yaml;"
        }

  
  stages{
      
    
       stage('build'){
            
         steps{
          
           sh "${mvnCMD} clean install"
         }
          
      }
      
      stage('send Artifacts to ansible'){
          steps{
             sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansiblehost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '//opt//docker', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: 'target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          }
      }
      
      stage('build image'){
          steps{
              sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansiblehost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: "cd /opt/docker; sudo ansible-playbook build.yaml;", execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          }
          
      }
      
      stage('create container'){
          steps{
              sshPublisher(publishers: [sshPublisherDesc(configName: 'Ansiblehost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo ansible-playbook container.yaml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
          }
      }
    
  }
}
    
