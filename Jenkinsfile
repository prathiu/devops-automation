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
         
         
            steps{
                script{
                    sh 'docker build -t prathiusha/devops-integration .'
                    withCredentials([string(credentialsId: 'docker', variable: 'docker')]) {
                    sh 'docker login -u javatechie -p ${docker}'
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
