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
withCredentials([usernamePassword(credentialsId: 'dockhub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {

echo "Packaging the code"

sh "scp -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.12.151:/home/ec2-user"
    sh "scp -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.12.151:/home/ec2-user"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 'bash ~/server-script.sh'"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 sudo docker build -t 28141108/java-mvn-privaterepos:$BUILD_NUMBER ."
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 sudo docker login -u $USERNAME -p $PASSWORD"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.12.151 sudo docker push 28141108/java-mvn-privaterepos:$BUILD_NUMBER"
    
}
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
    
