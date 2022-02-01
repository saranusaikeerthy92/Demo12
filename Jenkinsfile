pipeline {
    agent none
    tools {
        jdk 'myjava'
        maven 'mymaven'
    }
    stages{
        stage("Compile"){
            agent any
            steps{
                script{
                    echo "Compiling the code"
                    git 'https://github.com/saranusaikeerthy92/addressbook-1.git'
                    sh 'mvn compile'
                }
                
            }
            
        }
        
          stage("UnitTest"){
              agent {label 'linux_slave'}
              
            steps{
                script{
                    echo "Testing the unit test cases"
                    sh 'mvn test'
                }
                
            }
            
        }
        
          stage("Packaging"){
              agent any
                         steps{
                script{
                    echo "Packaging the code"
                    sshagent(['test-server-key']) {
                        
    sh "ssh -o StrictHOstKeyChecking=no ec2-user@172.31.12.151 'mvn package'"
}
                    sh 'mvn test'
                }
                
            }
            
        }
stage("Deploy"){
    agent any
            steps{
                script{
                    echo "Deploying the app"
                }
                
            }
            
        }      
      
        
    }
    
}
    
