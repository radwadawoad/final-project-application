pipeline {
    agent any
        stages {
          stage('Build') {
            steps {
                // Get some code from a GitHub repository
                 git branch: 'main',
                    url: 'https://github.com/AmiraRagab/GKE-simpleapp-deployed-byjenkins.git'

            }
        }
        stage('ci') {
            steps {
                  withCredentials([usernamePassword(credentialsId: 'dockerhub_key', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')])
                {
                    sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                    sh "docker build -t nodejs ."
                    sh "docker tag nodejs:latest amirayousef/nodejs"
                    sh "docker push amirayousef/nodejs"
                    
                }
            }    
        }
         stage ('deploy nodejs app'){
            steps {
            
                          sh """
                    #kubectl create namespace application    
                    kubectl apply -f deployment -n application
                    kubectl apply -f service.yml -n application
                echo Successful
            """
            }
        
        }
    }
}
