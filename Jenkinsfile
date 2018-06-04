node {


    checkout scm

    stage('Build Code'){
        sh '''#!/usr/bin/env bash
        mvn clean install package
        mvn docker:build
        '''

    }

    stage('Push image to registry'){
        
        sh("docker image push")
        
    }

    stage('Deploy Application'){


        sh("kubectl apply -f k8s/*")
                
    }



}