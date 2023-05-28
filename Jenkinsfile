pipeline {
    agent { label 'k8s_docker' }
  
      stages {
        stage('vcs') {
            steps{
                git branch: 'main',
                url: 'https://github.com/manohargatla/jenkins-k8s-deploy.git'
            }
            
        }
        stage('build image') {
            steps {
                sh "docker image build -t spc:${currentBuild.number} . "
                sh "docker tag spc:${currentBuild.number} manugatla/spc:${currentBuild.number}"
                sh "docker push manugatla/spc:${currentBuild.number}"
            }
        }
        stage('deploying application') {
            steps {
                sh 'sudo microk8s kubectl apply -f deployment.yaml'
                sh 'sudo microk8s kubectl get po'
                sh 'sudo microk8s kubectl get svc'
            }
        }
    }
}