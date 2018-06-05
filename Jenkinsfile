node {


    checkout scm
    withEnv(['DOCKER_HOST=unix:///var/run/docker.sock']){
        stage('Build Code'){
            sh '''#!/usr/bin/env bash
            echo $DOCKER_HOST
            mvn clean install package
            echo "$DOCKER_HOST 2"
            docker-compose build
            echo "$DOCKER_HOST 3"
            '''

        }
    }
    stage('Push Images to Repository'){
        sh '''
        export DOCKER_HOST=unix:///var/run/docker.sock
        docker login -u jmsv888 -p fiat500
        grep -i 'image:' docker-compose.yml | grep -i hygieia
        grep -oP '(?<=image: ).*' docker-compose.yml > images.out
        for i in `cat images.out`; do docker tag $i jmsv888/$i; docker push jmsv888/$i; done
        # cd ./k8s ; ls -lrt *.yaml | awk '{print $9}' > kubelist.out
        # for i in `cat kubelist.out`; do cat $i | grep image|cut -d ':' -f 2 >> image_name.out ; done
        # for i in `cat image_name.out` ; do docker push $i:latest; sleep 5 ; done
        '''

    }

    stage('Deploy Application'){


        sh("kubectl apply -f k8s/*.yaml")
                
    }



}
