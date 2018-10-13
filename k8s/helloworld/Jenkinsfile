pipeline {
    agent any
    stages {
        stage('deploy_hello_world') {
            steps {
                withKubeConfig(credentialsId: 'kube-local-test.config') {
                    sh '''kubectl create cm hello_world --dry-run --from-file=hello_world.py -o yaml > hello_world_cm.yaml
                          kubectl apply -f hello_world_cm.yaml

                          if [ `kubectl get job | grep hello_world | wc -l ` -gt 0 ]; then
                            kubectl delete job hello_world
                            sleep 10
                          fi 
                          kubectl apply -f hello_world_job.yaml'''
                }

            }
        }
    }
}