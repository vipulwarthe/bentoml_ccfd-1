node {
         stage("Git Clone"){

         git credentialsId: 'Git-hub-Credentials', url: "https://github.com/Devendra61/bentoml_ccfd.git"
         
         stage("Docker build"){
             sh 'docker version'
             sh 'pip install -r requirements.txt'
             sh 'python3 train.py'
             sh 'bentoml build .'
             sh 'bentoml containerize xgb_classifier:latest -t devbarahen61/xgb_classifier:latest'

         }

          withcredentials([string(credentialsid:'Docker-Hub-Password', variable: 'PASSWORD')]){
             sh 'docker login -u devbarahen61 p $PASSWORD'
          }

          stage("Push image to docker hub"){
             sh 'docker push devbarahen61/xgb_classifier:latest'
          }

          stage("Kubernetes deployment"){
             sh 'kubectl apply -f deploymentservice.yaml'
           }

           #stage("Cleanup resources"){                        
            # sh 'echo cleanup'
            # sh "docker rmi devbarahen61/xgb_classifier:${BUILD_NUMBER}"
            # sh "docker rmi devbarahen61"
            #}
        }
    }
