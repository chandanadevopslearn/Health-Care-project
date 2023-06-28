node{
    stage('git checkout')
    {
        git branch: 'master', url: 'https://github.com/Akhil2598/health-care-project.git'
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
    sh 'sudo docker build -t akhil2598/healthcare-project:1.0 .'
   
    }
    stage('docker image push to registry')
    {
    
    withCredentials([string(credentialsId: 'dockercred', variable: 'dockercred')]) {
        sh 'docker login -u akhil2598 -p ${dockercred}'
        sh 'docker push akhil2598/healthcare-project:1.0'
    
}
    }
    stage('deploy')
    {
       sh 'sudo chmod 777 /etc/ansible/akhil.pem'
       ansiblePlaybook become: true, credentialsId: 'akhil', disableHostKeyChecking: true, installation: 'myansible', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml' 
    }
}
