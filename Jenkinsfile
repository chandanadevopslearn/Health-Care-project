node{
    stage('git checkout')
    {
        git branch: 'master', url: 'https://github.com/chandanadevopslearn/Health-Care-project.git'
    }
    stage('compile using maven'){
    
    sh 'mvn clean compile'
    }
    stage('test using maven'){
        
    sh 'mvn clean test'
    }
    stage('package using maven'){
        
    sh 'mvn clean package'
    }
    stage('dockerimagebuild')
    {
    sh 'sudo docker build -t mchandana123/healthcare-project:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockercred', variable: 'dockercred')]) {
        sh 'docker login -u mchandana123 -p ${dockercred}'
        sh 'docker push mchandana123/healthcare-project:1.0'
    
}
    }
    stage('deploy')
    {
       sh 'sudo chmod 777 /etc/ansible/ansible.pem'
       ansiblePlaybook become: true, credentialsId: 'akhil', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
