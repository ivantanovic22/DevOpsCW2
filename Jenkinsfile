node {
    stage('Checkout') { // for display purposes
       checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'Github', url: 'https://github.com/ivantanovic22/DevOpsCW2.git']]])
    }
    stage('Build') {
      "building image from dockerfile" 
      sh '''#! /bin/bash

docker image build --tag ivantanovic22/server.js:1.0 .
'''
        
    }
    stage('Testing') {
    "Testing container is launched from image "
 sh '''#! /bin/bash

docker container run --detach --publish 80:80 --name server.js ivantanovic22/server.js:1.0

docker exec -it server.js sh


'''
sh '''#! /bin/bash

ls


'''
    }
    stage("Push image to dockerhub"){
    "pushing image to DockerHub"
    sh '''#! /bin/bash

docker push ivantanovic22/server.js:1.0


'''
    
    }
    stage("Deployment"){
    "deploying passed builds to kubernetes"
sh '''#! /bin/bash

kubectl set image deployments/server.js server.js=ivantanovic22/server.js:2.0


'''
        
    }
}
