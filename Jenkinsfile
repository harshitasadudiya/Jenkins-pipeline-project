pipeline {
    agent none  
    tools {
        maven 'maven3' 
    }

    stages {
        stage('Checkout') {
            agent { label 'master' }  
            steps {
                echo "Checking out code on master node..."
                checkout([$class: 'GitSCM',
                 branches: [[name: '*/main']],
                 userRemoteConfigs: [[url: 'https://github.com/vcjain/docker-agent-demo.git']]
                 ])
            }
        }

        stage('Build') {
            agent { label 'java' }  
            steps {
                echo "Compiling code on slave1 (java)..."
                sh 'mvn compile'
            }
        }

        stage('Test') {
            agent { label 'ssh' } 
            steps {
                echo "Running tests on slave2 (ssh)..."
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            agent { label 'master' } 
            steps {
                echo "Deploying from master node..."
            }
        }
    }
}
