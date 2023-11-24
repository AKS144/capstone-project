node{    
    stage('code checkout'){
        git 'https://github.com/AKS144/capstone-project.git'
    }    
    stage('code build'){
        sh 'mvn clean install'
    }    
    stage('containerize'){
        sh 'docker build -t abhi144k/insureme:1.0 .'
    }       
    stage('push on docker'){     
        withCredentials([string(credentialsId: 'dockerhubpsd', variable: 'dockerhubpsd')]) {
            sh "docker login -u abhi144k -p ${dockerhubpsd}"
            sh 'docker push abhi144k/insureme:1.0'
        }
    }  
    stage('deploy'){
    ansiblePlaybook become: true, disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml', vaultTmpPath: ''
    	
    }  
}
