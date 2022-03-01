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
                    echo "Compile the code"
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
sh "scp -o StrictHostKeyChecking=no server-script.sh ec2-user@172.31.24.126:/home/ec2-user"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.24.126 'bash ~/server-script.sh'"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.24.126 sudo docker build -t 28141108/java-mvn-privaterepos:$BUILD_NUMBER /home/ec2-user/addressbook-1"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.24.126 sudo docker login -u $USERNAME -p $PASSWORD"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.24.126 sudo docker push 28141108/java-mvn-privaterepos:$BUILD_NUMBER"
    
}
    }                    
                }
                
            }
            
        }
stage("Deploy"){
    agent any
            steps{
                script{
sshagent(['test-server-key']){
withCredentials([usernamePassword(credentialsId: 'dockhub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
echo "running the docker container"
sh "scp -o StrictHostKeyChecking=no ec2-user@172.31.0.51 sudo yum install docker -y"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.0.51 sudo systemctl start docker"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.0.51 sudo docker login -u $USERNAME -p $PASSWORD"
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.0.51 sudo docker run -itd -P 28141108/java-mvn-privaterepos:$BUILD_NUMBER"
                }
                
            }
            
        }      
      
        
    }
    
}
    
}
    }
