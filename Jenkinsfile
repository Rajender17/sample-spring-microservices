pipeline {
agent {
label 'Build-server'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; mvn clean install " 
    }
}
    stage ('dockerbuild') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo  docker login -uankit1111 -pmiet@1234 "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo docker tag account-service ankit1111/account-service  "
        sh "cd /home/ubuntu/workspace/Jenkins-Pipeline-java-ms/account-service ; sudo docker push ankit1111/account-service   "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node (' Ansible-server') {
             sh " sudo ansible-playbook /root/k8s.yaml"
             sh " sudo ansible-playbook /root/k8sservice.yaml" 
   
    }
}
}
}
    
    
}
