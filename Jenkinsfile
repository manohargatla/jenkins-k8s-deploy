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
                sh 'docker image build -t spc:2.0 .'
                sh 'docker tag spc:2.0 manugatla/spc:2.0'
                sh 'docker push manugatla/spc:2.0'
            }
        }
        stage('deploying application') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl get po'
                sh 'kubectl get svc'
            }
        }
    }
}