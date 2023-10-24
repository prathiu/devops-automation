pipeline {
    agent any
    tools{
        maven 'maven_3_9_5'
    }
    stages{
        stage('Build Maven'){
            steps{
              
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t prathiusha/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
         environment {
           DOCKERHUB-CREDENTIALS = credentials('docker')
             registry = "prathiusha/devops-integration"
               registryCredential = 'docker'
         }
            steps{
                script{
                    sh 'cd webapp && docker build -t prathiusha/devops-integration .'
                     sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                      sh 'docker push prathiusha/devops-integration'
}
                }
            }
        
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8')
                }
            }
        }
    }
}
