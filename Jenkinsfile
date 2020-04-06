node {
    def app

    stage('Clone repository') {
        /* repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* To builds the dockerimage */
        //update your ECR registry URI
        app = docker.build("gcr.io/mystic-impulse-245222/soloo0000")
    }

    stage('Test image') {
        /* Try killing some white walkers for testing ;-) */

        app.inside {
            sh 'echo "Container image successfully created "'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image */
        //docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
        // update your ECR registry URI and jenkins crendential paramater
        docker.withRegistry('https://gcr.io', 'gcr:mystic-impulse-245222')    {
            //app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }

    stage('create K8s cluster') {
             sh 'gcloud container clusters create --zone us-central1-a --network sanvpc mycluster --num-nodes=2'
        
    }
}
