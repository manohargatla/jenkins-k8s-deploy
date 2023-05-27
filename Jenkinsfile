pipeline {
    agent 'any'
      stages{
        stage('build image') {
            steps {
                sh 'docker image build -t nopcommerce:1.0 .'
                sh 'docker tag nopcommerce:1.0 manugatla/nopcommerce:1.0'
                sh 'docker push manugatla/nop:latest'
            }
        }
        stage('deploying application'){
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl get po'
                sh 'kubectl get svc'
            }
        }
    }
}