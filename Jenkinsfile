pipeline{
    agent any
    tools {
        maven "hello-world-maven"
    }
    stages{
        stage('pull the source code'){
            steps{
                echo 'pulling the source code'
                git branch: 'master', url: 'https://github.com/radhakuna/helloworld.git'
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
    }
}
