node {


    checkout scm

    stage('Build Code'){
        sh '''#!/usr/bin/env bash

        '''

    }

    stage('Build image'){
        sh("docker build -t ${imageTag} .")
    }

    stage('Push image to registry'){
        
        sh("gcloud docker -- push ${imageTag}")
        
    }

    stage('Deploy Application'){


                sh("kubectl --namespace=${env.BRANCH_NAME} apply -f k8s/services/")
                sh("kubectl --namespace=${env.BRANCH_NAME} apply -f k8s/qa/")
                //sh("echo http://`kubectl --namespace=develop get service/${feSvcName} --output=json | jq -r '.status.loadBalancer.ingress[0].ip'` > ${feSvcName}")

        
    }



}