pipeline {
    agent none

    tools {
      maven 'maven3'
    }
    
    
    stages{
        stage ('Checkout') {
             agent {
                   label 'master'
            }
            steps{
                checkout poll: false, scm: scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vcjain/docker-agent-demo.git']])
            }
            
        }
        stage ('Build') {
             agent {
                   label 'java'
             }
            steps {
                echo "Build Stage is in progress"
                sh 'mvn compile'
            }
            
        }
        stage ('Test'){
             agent {
                  label 'ssh'
            }
            steps {
                echo "Test Stage is in progress"
                sh 'mvn test'
            }
            
        }
        stage('Deploy'){
             agent {
                   label 'master'
            }
            steps{
                echo 'Deploying Build'
            }
        }
    }
}
