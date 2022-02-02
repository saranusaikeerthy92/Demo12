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
              agent any
              
            steps{
                script{
                    echo "Testing the unit test cases"
                    git 'https://github.com/saranusaikeerthy92/addressbook-1.git'
                    sh 'mvn test'
                }
                 
            }
            
        }
        
          stage("Packaging"){
              agent any
                         steps{
                script{
                    
                    sshagent(['test-server-key']){
                         echo "Packaging the code"

    sh "SCP -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.12.151:/home/ec2-user"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 'bash ~/server-script.sh'"

}                    
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
    
