node {
         stage("Git Clone"){

         git credentialsId: 'Git-Hub-Credentials', url: "https://github.com/vipulwarthe/bentoml_ccfd-1.git"
         
         stage("Docker build"){
             sh 'docker version'
             sh 'pip install -r requirements.txt'
             sh 'python3 train.py'
             sh 'bentoml build .'
             sh 'bentoml containerize xgb_classifier:latest -t vipulwarthe/xgb_classifier:latest'
         
         }
         stage("Docker Login"){
                   
             withCredentials([string(credentialsId: 'vipulwarthe', variable: 'PASSWORD')]) {
        	    sh "docker login -u vipulwarthe -p ${PASSWORD}"
         }
         }
         stage("Push image to docker hub"){
             sh 'docker push vipulwarthe/xgb_classifier:latest'
         }

         stage("Kubernetes deployment"){
             kubernetesDeploy (configs: 'deploymentservice.yaml', kubeconfigId: 'kuberneteskey')
           }

        }
    }
