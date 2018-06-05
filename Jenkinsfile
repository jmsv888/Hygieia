node {


    checkout scm

    stage('Build Code'){
        sh '''#!/usr/bin/env bash
        mvn clean install package
        docker-compose build
        '''

    }

    stage('Push Images to Repository'){
        sh '''
        docker login -u jmsv888 -p fiat500
        cd ./k8s ; ls -lrt *.yaml | awk '{print $9}' > kubelist.out
        for i in `cat kubelist.out`; do cat $i | grep image|cut -d ':' -f 2 >> image_name.out ; done
        for i in `cat image_name.out` ; do docker push $i:latest; sleep 5 ; done
        '''

    }

    stage('Deploy Application'){


        sh("kubectl apply -f k8s/*.yaml")
                
    }



}