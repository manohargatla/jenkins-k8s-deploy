pipeline {
    agent 'any'
  
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
                sh "docker tag spc:2.0 manugatla/spc:${currentBuild.number}"
                sh "docker push manugatla/spc:${currentBuild.number}"
            }
        }
        stage('deploying application') {
            steps {
                sh 'microk8s kubectl apply -f deployment.yaml'
                sh ' microk8s kubectl get po'
                sh 'microk8s kubectl get svc'
            }
        }
    }
}