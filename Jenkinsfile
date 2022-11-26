pipeline{
    agent any
    tools {
        maven "hello-world-maven"
    }
    stages{
        stage('pull the source code'){
            steps{
                echo 'pulling the source code'
                git branch: 'master', url: 'https://github.com/radhakuna/demo-java.git'
                echo '==============================='
                echo 'source code pulling completed'
                echo '==============================='
            }
        }
        stage('building the source code'){
            steps{
                echo 'starting the code build'
                sh 'mvn clean install'
            }
        }  
        
        stage('copying the docker to ansible'){
            steps{
                echo 'copying the docker'
                sshagent(['Ansible-Server']){
                    sh 'scp Docker-Ansible-file.yml ansible@172.31.86.169:/home/ansible/ci-cd-files'               
                    sh 'scp ./target/demo.war ansible@172.31.86.169:/home/ansible/ci-cd-files'
                    sh 'scp dockerplaybook.yml ansible@172.31.86.169:/home/ansible/ci-cd-files'
                  
                    sh '''
                     ssh -tt ansible@172.31.86.169 << EOF
                        ansible-playbook  ci-cd-files/dockerplaybook.yml
                     exit
                     EOF
                    '''
                }
            }
        }//CI Completed
    }
}
