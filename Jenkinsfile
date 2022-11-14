pipeline
{
    agent any
     stages {
      
        stage('Pulling Myapp from Git...') {
            steps {
                
                git branch: 'master', url: 'https://github.com/ahmedmaatki/projetcd-ja.git'          
            }
     
        }
        stage('install node_modules') {
            steps {
            sh ' npm install' 
            
            }
        }
       stage('install pip') {
            steps {
            sh 'pip3 install docker' 
            
            }
        }

        stage('Building Myapp...') {
            steps {
                script {
                    sh ' ansible-playbook ansible/build.yml -i ansible/inventory/host.yml '
                 }
            }
        }

        stage('Building docker image and running container') {
            steps {
                script {
                    sh ' ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml '
                 }
            }
        }


        stage('Pushing the created image to dockerhub') {
            steps {
                
                script {
                    sh ' ansible-playbook ansible/docker-registry.yml -i ansible/inventory/host.yml '
                 }
                 
            }
        }

        
     }
}
