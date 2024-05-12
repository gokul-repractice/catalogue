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
          zip -q -r catalogue.zip /.* -x '.git' -x '*.zip'
          ls -ltr
         """   
        }
    }
        
      
}
 post { 
        always { 
            echo 'I will always say Hello again!'
            
        }
        success { 
            echo 'I will always say success!'
        }
                failure { 
            echo 'I will always say success!'
        }
    }
    }