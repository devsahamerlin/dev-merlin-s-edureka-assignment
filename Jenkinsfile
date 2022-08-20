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
        /*stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t devsahamerlin/listingrestapi .'
                }
            }
        }
        stage('Push image to docker Hub'){
            steps{
                script{

                    withCredentials([string(credentialsId: 'jenkins-dockerhub-pwd', variable: 'jenkinsdockerhubpwd')]) {
                    sh 'docker login -u devsahamerlin -p ${jenkinsdockerhubpwd}'
                    }

                   sh 'docker push devsahamerlin/listingrestapi'
                }
            }
        }*/
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'localk8sconfigpwd')
                }
            }
        }
    }
}