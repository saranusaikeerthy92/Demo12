pipeline {
    agent any 
parameters{
    string(name: 'Env',defaultValue:'1:1',description:'version to deploy')
    booleanParam(name:'executeTests',defaultValue: true, description: 'decide to run tc')
    choice(name:'APPVERSION',choices:['1:1','1:2','1:3'])
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
        
          stage("Packing "){
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
    when {
        expression{
            BRANCH_NAME=='master'
        }
    }
            steps{
                script{
                    echo "Deploying the app"
                    echo "deploying version ${params.Env}"
                    echo "deploying the app version ${params.APPVERSION}"
                }
                
            }
            
        }      
      
        
    }
    
}
    
