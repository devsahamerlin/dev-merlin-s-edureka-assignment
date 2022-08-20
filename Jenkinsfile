pipeline {
    agent any
    tools{
        maven 'Maven_3_8_6'
    }
    stages{
        stage('Check jdk version'){
            steps{
                script{
                    sh 'java -version'
                }
            }
        }
        stage('Maven Compile'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/swmproopengit/devsahaMerlinListingTest']]])
                sh 'mvn clean install'
            }
        }
        stage('Maven Build And Test'){
             steps{
                 checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/swmproopengit/devsahaMerlinListingTest']]])
                 sh 'mvn clean install'
             }
         }

        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'localk8sconfigpwd')
                }
            }
        }
    }
}