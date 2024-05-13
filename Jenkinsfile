pipeline{
    agent{
         node {
        label 'agent-1'
    }
    }
    options {
        timeout(time: 1, unit: 'HOURS') 
         disableConcurrentBuilds()
    }
    environment { 
        package_version = ''
        nexus_url = 'http://172.31.5.248:8081/repository'
    }
    stages{
         stage("get version")
         {
        steps{
             
           script{
            def file = readJSON file: 'package.json'
            package_version = file.version
            echo "${package_version}"
           }
            }
         }
        stage("install dependencies")
         {
        steps{
         sh """    
            npm install  
         """   
        }
    }
     stage("build")
         {
        steps{
         sh """    
          ls -la
          zip -q -r catalogue.zip ./* -x '.git' -x '*.zip'
          ls -ltr
         """   
        }
    }
    stage("deploy")
         {
                steps {
                          nexusArtifactUploader(
                            nexusVersion: 'nexus3',
                                protocol: 'http',
                           nexusUrl: '${nexus_url}',
                            groupId: 'com.roboshop',
                            version: '${package_version}',
                            repository: 'catalogue',
                            credentialsId: 'nexus-id',
                             artifacts: [
                               [artifactId: 'catalogue',
                                 classifier: '',
                                    file: 'catalogue.zip',
                              type: 'zip']
                                ]
                            )
                         }        
         } 
}
 post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir()
        }
        success { 
            echo 'I will always say success!'
        }
                failure { 
            echo 'I will always say success!'
        }
    }
}