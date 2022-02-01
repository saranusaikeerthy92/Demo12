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

    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 'sudo yum install java-1.8.0-openjdk-devel -y'"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 'sudo yum install git -y'"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 'sudo yum install maven -y'"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 '/home/ec2-user/addressbook-1/'"
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
    
