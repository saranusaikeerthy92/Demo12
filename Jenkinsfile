pipeline {
    agent any
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    stages{
        stage("Compile"){
            steps{
                script{
                    echo "Compiling the code"
                    git 'https://github.com/saranusaikeerthy92/addressbook-1.git'
                    sh 'mvn compile'
                }
                
            }
            
        }
        
          stage("UnitTest"){
              
              
            steps{
                script{
                    echo "Testing the unit test cases"
                    sh 'mvn test'
                }
                
            }
            
        }
        
          stage("Packaging"){
             
            steps{
                script{
                    echo "Packaging the code"
                    sh 'mvn test'
                }
                
            }
            
        }
stage("Deploy"){
    
            steps{
                script{
                    echo "Deploying the app"
                }
                
            }
            
        }      
      
        
    }
    
}
    
