pipeline {
    agent any 
parameters{
    string(name: 'Env',defaultValue:'Test',description:'version to deploy')
    booleanParam(name:'executeTests',defaultValue: true, description: 'decide to run tc')
    choice(name:'BRANCH',choices:['1:1','1:2','1:3'])
}   
environment{
    NEW_VERSION ='2.1'
}
    stages{
        stage("Compile"){
            steps{
                script{
                    echo "Compiling the code"
                }
                
            }
            
        }
        
          stage("UnitTest"){
              when {
                  expression {
                      params.executeTests == true
                  }
              }
            steps{
                script{
                    echo "Testing the unit test cases"
                }
                
            }
            
        }
        
          stage("Packing"){
              input {
                  message "Select the version to package"
                  ok "Package version is selected"
                  parameters{
                      choice (name:'NEWAPP',choices:['1.2','2.1','3.1'])
                  }
              }
            steps{
                script{
                    echo "Packaging the code"
                    echo "Packaging version ${NEW_VERSION}"
                }
                
            }
            
        }
stage("Deploy"){
    
            steps{
                script{
                    echo "Deploying the app"
                    echo "Deploying version ${params.Env}"
                    echo "Deploying the app version ${params.APPVERSION}"
                }
                
            }
            
        }      
      
        
    }
    
}
    
