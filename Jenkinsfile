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
                    sh 'scp ./target/demo.war ansible@172.31.90.178:/home/ansible/ci-cd-files'
                    sh 'scp dockerplaybook.yml ansible@172.31.90.178:/home/ansible/ci-cd-files'
                    sh 'scp Dockerfile.yml ansible@172.31.85.209:/home/ansible/ci-cd-files'
                  
                    sh '''
                     ssh -tt ansible@172.31.90.178 << EOF
                        ansible-playbook  ci-cd-files/dockerplaybook.yml
                     exit
                     EOF
                    '''
                }
            }
        }//CI Completed
    }
}
