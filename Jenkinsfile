node {
    def app

    environment {
            image_name =
            DB_ENGINE    = 'sqlite'
    }
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        /*checkout scm*/
        sh 'echo $giturl'
    }




    stage('Build image') {

         sh 't=`echo $giturl  | awk -F/ '{print $NF}' | awk -F. '{print $1}`'
         sh 'echo "TEST=$t" > envFile.properties'
        app = docker.build("fatninja/$TEST")
       sh 'echo $HELLO'
    }

    stage('Test image') {


        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {

        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
