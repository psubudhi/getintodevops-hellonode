node {
    def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */
        // git clone --recursive https://github.com/KyleFinley1/getintodevops-hellonode.git kubernetes_cookbook_2ed
        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        /* app = docker.build("getintodevops/hellonode") */
        app = docker.build("getintodevops/hellonode")
    }
    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'hub.docker') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
